# **BBQ_Planner_T3A2-b_Back-end**

# **End Points:**

#### **Get All participants:**

```JSON
[
    {
        "_id": "63d06ab35489f93f1ae35627",
        "name": "Johnny",
        "drink_id": "63d06ab35489f93f1ae35623",
        "meat_eater": "No",
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae35628",
        "name": "Karen",
        "drink_id": "63d06ab35489f93f1ae35623",
        "meat_eater": "Yes",
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae35629",
        "name": "Angela",
        "drink_id": "63d06ab35489f93f1ae35624",
        "meat_eater": "No",
        "__v": 0
    }
]

```

#### **Get, Put, Delete participant by id:**

```JSON
[
    {
        "_id": "63d06ab35489f93f1ae35627",
        "name": "Johnny",
        "drink_id": "63d06ab35489f93f1ae35623",
        "meat_eater": "No",
        "__v": 0
    }
]

```

#### **Get All beverages Seeded and Neverchanging:**

```JSON

[
    {
        "_id": "63d06ab35489f93f1ae35622",
        "name": "Beer",
        "quantity": 2,
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae35623",
        "name": "Wine",
        "quantity": 1,
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae35624",
        "name": "Juice",
        "quantity": 1,
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae35625",
        "name": "Softdrink",
        "quantity": 2,
        "__v": 0
    }
]

```

#### **Get All foods Seeded and Neverchanging:**

```JSON

[
    {
        "_id": "63d06ab35489f93f1ae3562c",
        "name": "Beef",
        "quantity": 0.3,
        "cont_meat": "Yes",
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae3562d",
        "name": "Sausage",
        "quantity": 0.3,
        "cont_meat": "Yes",
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae3562e",
        "name": "Potato Salad",
        "quantity": 0.3,
        "cont_meat": "No",
        "__v": 0
    },
    {
        "_id": "63d06ab35489f93f1ae3562f",
        "name": "Veg Sausage",
        "quantity": 0.3,
        "cont_meat": "No",
        "__v": 0
    }
]

```

# **Testing:**

#### **End to End Automated testing:**

 - The type of testing we have decided to perform is the Automated End to End testing and the technology chosen to perform the test is the jest and supertest dependencies. The testing code covers an array of scenarios such as Getting Home Page, Creating a new participant, getting a participant's list and checking the quantity of elements and its data structure. Getting a beverage's list and checking the quantity of elements and its data structure. Getting a food's list and checking the quantity of elements and its data structure.
    An "app.test.js" file was created containing the following code that was run using the command "npm test":

```javascript

import app from './app.js'
import request from 'supertest'

describe("App tests", () => {
    test('Get Home Page', async () => {
    const res = await request(app).get('/')
    expect(res.status).toBe(200)
    expect(res.body.info).toBeDefined()
    expect(res.body.info).toBe('Barbecue Planner API')
})

describe('Get Participants list', () => {
    let res

    beforeEach(async () => {
        res = await request(app).get('/participants')
        expect(res.status).toBe(200)
    })
    it('Return an array with 6 elements', () => {
        expect(res.body).toBeInstanceOf(Array)
        expect(res.body.length).toBe(6)
    })
    it('it has the correct data-structure', () => {
        res.body.forEach(it => {
            expect(it._id).toBeDefined()
            expect(it.name).toBeDefined()
            expect(it.drink_id).toBeDefined()
            expect(it.meat_eater).toBeDefined()
            expect(it._id.length).toBe(24)
        })
        expect(res.body[0].name).toBe('John')
    })
})

describe('Get Beverages list', () => {
    let res

    beforeEach(async () => {
        res = await request(app).get('/beverages')
        expect(res.status).toBe(200)
    })
    it('Return an array with 4 elements', () => {
        expect(res.body).toBeInstanceOf(Array)
        expect(res.body.length).toBe(4)
    })
    it('it has the correct data-structure', () => {
        res.body.forEach(it => {
            expect(it._id).toBeDefined()
            expect(it.name).toBeDefined()
            expect(it.quantity).toBeDefined()
            expect(it._id.length).toBe(24)
        })
        expect(res.body[0].name).toBe('Beer')
    })
})

describe('Get Foods list', () => {
    let res

    beforeEach(async () => {
        res = await request(app).get('/foods')
        expect(res.status).toBe(200)
    })
    it('Return an array with 4 elements', () => {
        expect(res.body).toBeInstanceOf(Array)
        expect(res.body.length).toBe(4)
    })
    it('it has the correct data-structure', () => {
        res.body.forEach(it => {
            expect(it._id).toBeDefined()
            expect(it.name).toBeDefined()
            expect(it.quantity).toBeDefined()
            expect(it.cont_meat).toBeDefined()
            expect(it._id.length).toBe(24)
        })
        expect(res.body[0].name).toBe('Beef')
    })
})

test('Create new Participant', async () => {
    const res = await request(app).post('/participants').send({
        name: 'Daniel',
        drink_id: '63d32fd81c20cfb6b245eeac',
        meat_eater: 'Yes'
    })
    expect(res.status).toBe(201)
    expect(res.body._id).toBeDefined()
    expect(res.body.name).toBeDefined()
    expect(res.body.drink_id).toBeDefined()
    expect(res.body.meat_eater).toBeDefined()
    expect(res.body.name).toBe('Daniel')
    expect(res.body.drink_id._id).toBe('63d32fd81c20cfb6b245eeac')
    expect(res.body.meat_eater).toBe('Yes')
})

})

```

#### **The Test Result after running "npm test"**

![End to end test results](./images/testing.jpg)

