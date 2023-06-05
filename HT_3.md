# Postman HW_3
___

#### EP_1 
Need to log in
POST
http://162.55.220.72:5005/login
login : str (кроме /)
password : str

The incoming token must be passed to all other requests

    let resp = pm.response.json()

    let respToken = resp.token

    pm.environment.set("auth_token", respToken);

##### All further requests require a token
___
#### EP_2

http://162.55.220.72:5005/user_info
req. (RAW JSON)
POST
age: int
salary: int
name: str
auth_token


    resp.
    {'start_qa_salary':salary,
    'qa_salary_after_6_months': salary * 2,
    'qa_salary_after_12_months': salary * 2.9,
    'person': {'u_name':[user_name, salary, age],
                                    'u_age':age,
                                    'u_salary_1.5_year': salary * 4}
                                    }

##### Tests:
##### 1. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

##### 2. Check the json structure in the answer.

    let jsonData = pm.response.json();

    pm.test("Check json structure", () => {
        pm.response.to.have.jsonSchema(jsonData)
    })
or

    let data1 = [true, false];
    let data2 = [true, 123];

    pm.test('Schema is valid', function () {
        pm.expect(tv4.validate(data1, jsonData)).to.be.true;
        pm.expect(tv4.validate(data2, jsonData)).to.be.true;
    });

##### 3. Answer contains multiplication coefficients of `salary`, write tests to check if the result of multiplication is correct by the coefficient.

    let req = JSON.parse(request.data)

    pm.test("Check salary multiplication", () => {
        pm.expect(jsonData.qa_salary_after_6_months).to.eql(req.salary * 2);
        pm.expect(jsonData.qa_salary_after_12_months).to.eql(req.salary * 2.9);
        pm.expect(jsonData.person.u_salary_1_5_year).to.eql(req.salary * 4);
    })

##### 4. Get the value from the field 'u_salary_1.5_year' and pass it to the query's salary field http://162.55.220.72:5005/get_test_user

    pm.environment.set("u_salary_1_5_year", jsonData.person.u_salary_1_5_year);


    pm.sendRequest({
        url: 'http://162.55.220.72:5007/get_test_user',
        method: 'POST',
        body: {
            mode: 'formdata',
            formdata: 
            { key: 'salary', value: pm.environment.get("u_salary_1_5_year")}
        }
        }, (error, response) => {
            if (error) {
                console.log(error);
            }

    pm.test('response should be okay to process', () => {
        pm.expect(error).to.equal(null);
        pm.expect(response).to.have.property('code', 200);
        pm.expect(response).to.have.property('status', 'OK');
    });
    });

___
#### EP_3 

http://162.55.220.72:5005/new_data
req.
POST
age: int
salary: int
name: str
auth_token

    Resp.
    {'name':name,
    'age': int(age),
    'salary': [salary, str(salary*2), str(salary*3)]}

##### Tests:
##### 1. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

##### 2. Check the json structure in the answer

    let jsonData = pm.response.json();

        pm.test("Check json structure", () => {
            pm.response.to.have.jsonSchema(jsonData)
        })

##### 3. Answer has multiplication coefficients of salary, write tests to verify that the result of multiplication by a factor is correct

    pm.test("Check 2 salary element", () => {
    pm.expect(jsonData.salary[2] > (jsonData.salary[1] && jsonData.salary[0])).to.have.true
    })

##### 4. Check that the 2nd element of the array is greater than the 1st and 0

    pm.test("Check 2 salary element", () => {
        pm.expect(+jsonData.salary[2]).to.be.greaterThan(jsonData.salary[1] && jsonData.salary[0])
    })
or

    pm.test("Check 2 salary element", () => {
        pm.expect(jsonData.salary[2] > (jsonData.salary[1] && jsonData.salary[0])).to.be.true
    })
___

#### EP_4 
http://162.55.220.72:5005/test_pet_info
req.
POST
age: int
weight: int
name: str
auth_token

    Resp.
    {'name': name,
    'age': age,
    'daily_food':weight * 0.012,
    'daily_sleep': weight * 2.5}


##### Tests:
##### 1. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

##### 2. Check the json structure in the answer

    let jsonData = pm.response.json();

    var data1 = [true, false];
    var data2 = [true, 123];

    pm.test('Schema is valid', function () {
        pm.expect(tv4.validate(data1, jsonData)).to.be.true;
        pm.expect(tv4.validate(data2, jsonData)).to.be.true;
    });
##### 3. The answer contains multiplication coefficients of weight, write tests to verify that the result of multiplication by a factor is correct

    let reqst = request.data
    pm.test("Check weight multiplication", function () {
        pm.expect(jsonData.daily_food).to.eql(reqst.weight * 0.012);
        pm.expect(jsonData.daily_sleep).to.eql(reqst.weight * 2.5)
    });

===================

#### EP_5 
http://162.55.220.72:5005/get_test_user
req.
POST
age: int
salary: int
name: str
auth_token

    Resp.
    {'name': name,
    'age':age,
    'salary': salary,
    'family':{'children':[['Alex', 24],['Kate', 12]],
    'u_salary_1.5_year': salary * 4}
    }

Tests:
##### 1. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

##### 2. Check the json structure in the response.

    let jsonData = pm.response.json()
    var data1 = [true, false];
    var data2 = [true, 123];

    pm.test('Schema is valid', function () {
        pm.expect(tv4.validate(data1, jsonData)).to.be.true;
        pm.expect(tv4.validate(data2, jsonData)).to.be.true;
    });

##### 3. Check that name field value = name variable value from environment

    pm.test("Check names", function () {
        pm.expect(jsonData.name).to.eql(pm.environment.get("name"));
    });


##### 4. Check if the value of age field in the response corresponds to the value of age field sent in the query

    let req = request.data
    pm.test("Check age", function () {
        pm.expect(jsonData.age).to.eql(req.age);
    });
___

#### EP_6 
http://54.157.99.22:80/currency
req.
POST
auth_token

    Resp. A list of an array of objects is passed.
        [
        {"Cur_Abbreviation": str,
        "Cur_ID": int,
        "Cur_Name": str
        }
        …
        {"Cur_Abbreviation": str,
        "Cur_ID": int,
        "Cur_Name": str
        }
        ]

##### Tests:
##### 1. You can take any object from the list sent, use js random. In the object take Cur_ID and pass it through the environment in the next query.

    let resp = pm.response.json()

    let numbberOfObject = Math.floor(Math.random() * resp.length) 
    let obj = resp[numbberOfObject]

    console.log(numbberOfObject)
    console.log(obj)

    pm.environment.set("Cur_ID", obj.Cur_ID);
___

#### EP_7. http://162.55.220.72:5005/curr_byn
req.
POST
auth_token
curr_code: int

    Resp.
    {
        "Cur_Abbreviation": str
        "Cur_ID": int,
        "Cur_Name": str,
        "Cur_OfficialRate": float,
        "Cur_Scale": int,
        "Date": str
    }

##### Tests:
##### 1. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

##### 2. Check the json structure in the response.

    var schema = pm.response.json()
    var data1 = [true, false];
    var data2 = [true, 123];

    pm.test('Schema is valid', function () {
        pm.expect(tv4.validate(data1, schema)).to.be.true;
        pm.expect(tv4.validate(data2, schema)).to.be.true;
    });

### ***
##### 1. obtain list of currencies
##### 2. iterate the list of currencies
##### 3. At each iteration send a request to the server for a rate for each currency
##### 4. if 500 code is returned, proceed to the next iteration
##### 5. if we get 200 code, we check the response json for "Cur_OfficialRate" field
##### 6. if the field is present, write the information about the falut in the console as a response
>{
    "Cur_Abbreviation": str,
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}


    let resp = pm.response.json()

    for (i = 0; i < resp.length; i++) {
        const currReq = ({
            url: "http://54.157.99.22:80/curr_byn",
            method: "POST",
            body: {
                mode: 'formdata',
                formdata: [
                    { key: 'auth_token', value: pm.environment.get("auth_token")},
                    { key: 'curr_code', value: `${resp[i].Cur_ID}`}
                ]
            }
        });
        pm.sendRequest(currReq, (error, response) => {
            let jsonData = response.json()
            console.log(jsonData.Cur_ID)
            pm.test("Check Cur_OfficialRate", function () {
                pm.expect(jsonData).to.property('Cur_OfficialRate');
            });
            console.log(jsonData)

        })
    }
##### 7. go to the next iteration

