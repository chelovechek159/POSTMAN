# Postman HW_1

___
### EP_1

#### 1. Send a request.

http://162.55.220.72:5005/first

#### 2. Status code 200

    pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
    });

#### 3. Check that the correct string comes in body

    pm.test("Body matches string", function () {
        pm.expect(pm.response.text()).to.include("This is the first responce from server!ss");
    });

### EP_2

#### 1. Send a request.

http://162.55.220.72:5005/user_info_3

#### 2. Status code 200

    pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
    });
#### 3. Parse response body to json

    let respData = pm.response.json()

#### 4. Check that the `name` in the response is equal to `name` in request (type in the name with your hands)

    pm.test("Check name", function () {
        pm.expect(respData.name).to.eql('Yarik');
    });

#### 5. Check that the `age` in the response is equal to `age` in request (type age with your hands)

    let age1 = +respData.age

    pm.test("Check age", function () {
        pm.expect(age1).to.eql(27);
    });

#### 6. Check that the `salary` in the response is equal to `salary` in request (salary type in with your hands)

    pm.test("Check salary", function () {
        pm.expect(respData.salary).to.eql(1000);
    });

#### 7. Parse request

    let reqData = request.data

#### 8. Check that `name` in the response is equal to `name` in request (pick name from request)

    pm.test("Check in Request name", function () {
        pm.expect(respData.name).to.eql(reqData.name)
    })

#### 9. Check that the `age` in the response is equal to `age` in request (take age from request)

    let age2 = +reqData.age

    pm.test("Check in Request age", function () {
        pm.expect(age1).to.eql(age2)
    })

#### 10. Check that the `salary` in the response is equal to `salary` in request (pick salary from request)

    let salary_1 = +reqData.salary

    pm.test("Check in Request salary", function () {
        pm.expect(respData.salary).to.eql(salary_1)
    })

#### 11. Output the `family` parameter from response to the console

    console.log(respData.family)

#### 12. Check that `u_salary_1_5_year` in response is equal to `salary * 4` (pick salary from request)

    pm.test("Check 'u_salary_1_5_year' * 4", function () {
        pm.expect(respData.family.u_salary_1_5_year).to.eql(salary_1 * 4)
    })

### EP_3

#### 1. Submit a request

    http://162.55.220.72:5005/object_info_3

#### 2. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

#### 3. Parse response body into json

    let respBody = pm.response.json()

#### 4. Parse request

    let reqData = pm.request.url.query.toObject()

#### 5. Check that the `name` in the response is equal to `name` s request (take name from request.)

    pm.test("Check name", function () {
        pm.expect(respBody.name).to.eql(reqData.name);
    });

#### 6. Check that the `age` in the response is equal to `age` s request (take age from request.)

    pm.test("Check age", function () {
        pm.expect(respBody.age).to.eql(reqData.age);
    });

#### 7. Check that the `salary` in the response is equal to `salary` s request (pick salary from request)

    pm.test("Check salary", function () {
        pm.expect(respBody.salary).to.eql(Number(reqData.salary));
    });

#### 8. Print the `family` parameter from response to the console

    console.log(respBody.family)
#### 9. Check that the `dog` parameter has `name` parameters

    let dogs = respBody.family.pets.dog

    pm.test("Check that dog has a name", function () {
        pm.expect(dogs).to.property("name");
    });

#### 10. Check that the `dog` parameter has `age` parameters

    pm.test("Check that dog has an age", function () {
        pm.expect(dogs).to.property("age");
    });

#### 11. Check that the `name` parameter is set to `Luky`

    pm.test("Check that dogs name has a name: 'Luky'", function () {
        pm.expect(dogs.name).to.eql("Luky");
    });

#### 12. Check that the `age` parameter is `4`

    pm.test("Check that dogs age has a value: 4", function () {
        pm.expect(dogs.age).to.eql(4);
    });

### EP_4

#### 1. Send a request
http://162.55.220.72:5005/object_info_4
#### 2. Status code 200

    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });
#### 3. Parse response body into json

    let respBody = pm.response.json()
#### 4. Parse request

    let reqData = pm.request.url.query.toObject()
#### 5. Check that the `name` in the response is equal to `name` s request (take name from request)

    pm.test("Check name", function () {
        pm.expect(respBody.name).to.eql(reqData.name);
    });

#### 6. Check that the `age` in the response is equal to the `age` from request (take age from request)

    pm.test("Check age", function () {
        pm.expect(respBody.age).to.eql(Number(reqData.age));
    });

#### 7. Print the `salary` parameter from request to the console

    console.log(reqData.salary)

#### 8. Print the `salary` parameter from response to the console

    console.log(respBody.salary)

#### 9. Print the [0] element of the `salary` parameter from response to the console

    console.log(respBody.salary[0])

#### 10. Print to the console the [1] element of the `salary` parameter, the salary parameter from response

    console.log(respBody.salary[1])

#### 11. Print to the console the [2] element of the `salary` parameter, the salary parameter from response

    console.log(respBody.salary[2])

#### 12. Check that [0] element of the `salary` parameter is equal to the `salary` from request (salary pick up from request)

    pm.test("Check salary_0", function () {
        pm.expect(respBody.salary[0]).to.eql(Number(reqData.salary));
    });

#### 13. Check that the [1] element of the `salary` parameter is equal to `salary * 2` from request (pick salary from request)

    pm.test("Check salary_1", function () {
        pm.expect(Number(respBody.salary[1])).to.eql(reqData.salary * 2);
    });

#### 14. Check that the [2] element of the `salary` parameter is equal to `salary * 3` from request (pick salary from request)

    pm.test("Check salary_2", function () {
        pm.expect(Number(respBody.salary[2])).to.eql(reqData.salary * 3);
    });

#### 15-17 Create a variable `name, age, salary` in the environment
https://drive.google.com/file/d/1Nq6hVjdEzabGEefdsqcYQey_eHiUfVvJ/view?usp=sharing
#### 18. Pass the `name` variable to the environment

    pm.environment.set("name", respBody.name);

#### 19. Pass the `age` variable to the environment

    pm.environment.set("age", respBody.age);

#### 20. Pass the `salary` variable to the environment

    pm.environment.set("salary", respBody.salary[0]);

#### 21. Write a loop that will output the list elements from the `salary` parameter to the console in order

    for (let i in respBody.salary){
        console.log([i] + ': ' + respBody.salary[i])
    }