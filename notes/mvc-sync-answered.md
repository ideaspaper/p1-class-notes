[**Back to Home**](./../README.md)

# MVC Sync Answered

Struktur Folder

```
.
├── app-db.json
├── controllers
│   └── Controller.js
├── index.js
├── models
│   ├── CustomerFactory.js
│   ├── Customer.js
│   ├── CustomerRegular.js
│   ├── CustomerVIP.js
│   └── Model.js
└── views
    └── View.js
```

`Controller.js`

```javascript
const View = require('./../views/View');
const Model = require('./../models/Model');

class Controller {
  static help() {
    View.help();
  }

  static create(name, age, privilege) {
    const data = Model.create(name, age, privilege);
    View.create(data);
  }

  static read() {
    const data = Model.read();
    View.read(data);
  }

  static update(id, name, age, privilege) {
    const data = Model.update(id, name, age, privilege);
    View.update(data);
  }

  static remove(id) {
    const data = Model.remove(id);
    View.remove(data);
  }
}

module.exports = Controller;
```

`CustomerFactory.js`

```javascript
const CustomerRegular = require('./CustomerRegular');
const CustomerVIP = require('./CustomerVIP');

class CustomerFactory {
  static create(id, name, age, type) {
    if (type === 'Regular') {
      return new CustomerRegular(id, name, age);
    } else if (type === 'VIP') {
      return new CustomerVIP(id, name, age);
    }
  }
}

module.exports = CustomerFactory;
```

`Model.js`

```javascript
const fs = require('fs');
const CustomerFactory = require('./CustomerFactory');

class Model {
  static create(name, age, privilege) {
    age = Number(age);
    const customers = Model.read();

    let userId = 1;
    if (customers.length > 0) {
      userId = customers[customers.length - 1].id + 1;
    }

    const newCustomer = CustomerFactory.create(userId, name, age, privilege);
    customers.push(newCustomer);
    fs.writeFileSync('./app-db.json', JSON.stringify(customers, null, 2));
    return newCustomer;
  }

  static read() {
    const data = JSON.parse(fs.readFileSync('./app-db.json', 'utf8'));

    const mappedData = data.map((each) => {
      return CustomerFactory.create(Number(each.id), each.name, Number(each.age), each.privilege);
    });

    return mappedData;
  }

  static update(id, name, age, privilege) {
    id = Number(id);
    age = Number(age);
    const customers = Model.read();
    let customerFoundIndex = -1;
    const customerFound = customers.find((each, index) => {
      if (each.id === id) {
        customerFoundIndex = index;
        return each;
      }
    });

    if (customerFoundIndex === -1) {
      return false;
    }

    const customerUpdate = CustomerFactory.create(id, name, age, privilege);
    customers[customerFoundIndex] = customerUpdate;

    fs.writeFileSync('./app-db.json', JSON.stringify(customers, null, 2));
    return [customerFound, customerUpdate];
  }

  static remove(id) {
    id = Number(id);
    const customers = Model.read();
    let customerFoundIndex = -1;
    const customerFound = customers.find((each, index) => {
      if (each.id === id) {
        customerFoundIndex = index;
        return each;
      }
    });

    if (customerFoundIndex === -1) {
      return false;
    }

    customers.splice(customerFoundIndex, 1);
    fs.writeFileSync('./app-db.json', JSON.stringify(customers, null, 2));
    return customerFound;
  }
}

module.exports = Model;
```

`View.js`

```javascript
class View {
  static help() {
    let helpString = 'Available commands:\n';
    helpString += '  - help\n';
    helpString += '  - create <name> <age> <privilege>\n';
    helpString += '  - read\n';
    helpString += '  - update <id> <name> <age> <privilege>\n';
    helpString += '  - remove <id>';

    console.log(helpString);
  }

  static create(data) {
    console.log('CREATE OPERATION');
    console.log('Successfully created:', data);
  }

  static read(data) {
    console.log('READ OPERATION');
    console.log(data);
  }

  static update(data) {
    console.log('UPDATE OPERATION');
    if (!data) {
      console.log('No data found');
    } else {
      console.log('Old data:', data[0]);
      console.log('New data:', data[1]);
    }
  }

  static remove(data) {
    console.log('REMOVE OPERATION');
    if (!data) {
      console.log('No data found');
    } else {
      console.log('Removed data:', data);
    }
  }
}

module.exports = View;
```

`index.js`

```javascript
const argv = process.argv;
const Controller = require('./controllers/Controller');

const command = argv[2];
const params = argv.slice(3);

if (command === 'help' || !command) {
  Controller.help();
} else if (command === 'create') {
  Controller.create(params[0], params[1], params[2]);
} else if (command === 'read') {
  Controller.read();
} else if (command === 'update') {
  Controller.update(params[0], params[1], params[2], params[3]);
} else if (command === 'remove') {
  Controller.remove(params[0]);
}
```

[**Back to Home**](./../README.md)