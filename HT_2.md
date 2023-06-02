# Postman HW_2

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

#### 1. Send a request

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

#### 15-17. Create a variable `name, age, salary` in the environment
![ScreenShoot](https://github.com/chelovechek159/Images/blob/main/Screenshot%202023-06-02%20at%2019.42.33.png)
#### 18-20. Pass the `name, age, salary` variable to the environment

    pm.environment.set("name", respBody.name);
    
    pm.environment.set("age", respBody.age);

    pm.environment.set("salary", respBody.salary[0]);

#### 21. Write a loop that will output the list elements from the `salary` parameter to the console in order

    for (let i in respBody.salary){
        console.log([i] + ': ' + respBody.salary[i])
    }

### EP_5

#### 1-3. Insert the `salary, age, name` parameters from the environment into request

#### 4. Send a request

http://162.55.220.72:5005/user_info_2

#### 5. Status code 200

    pm.test("Status code is 200", function () {
            pm.response.to.have.status(200);
        });

#### 6. Parse response body to json

    let respData = pm.response.json()

#### 7. Parse request.

    let reqData = request.data

#### 8. Check json response has start_qa_salary parameter

    pm.test("Check start_qa_salary", function () {
        pm.expect(respData).to.property("start_qa_salary");
    });

#### 9. Check that json response has parameter qa_salary_after_6_months

    pm.test("Check 6_Month_qa_salary", function () {
        pm.expect(respData).to.property("qa_salary_after_6_months");
    });

#### 10. Check json response has qa_salary_after_12_months parameter

    pm.test("Check 12_month_qa_salary", function () {
        pm.expect(respData).to.property("qa_salary_after_12_months");
    });


#### 11. Check json response has qa_salary_after_1.5_year parameter

    pm.test("Check 1.5_month_qa_salary", function () {
        pm.expect(respData).to.property("qa_salary_after_1.5_year");
    });

#### 12. Check json response has qa_salary_after_3.5_years parameter

    pm.test("Check 3.5_month_qa_salary", function () {
        pm.expect(respData).to.property("qa_salary_after_3.5_years");
    });

#### 13. Check json response has person parameter

    pm.test("Check person", function () {
        pm.expect(respData).to.property("person");
    });

#### 14. Check that the start_qa_salary parameter is equal to salary from request (pick salary from request)

    pm.test("Check salary", function () {
        pm.expect(respData.start_qa_salary).to.eql(Number(reqData.salary));
    });

#### 15. Check that the qa_salary_after_6_months parameter is equal to salary*2 from request (pick salary from request)

    pm.test("Check 6MonthSalary", function () {
        pm.expect(respData.qa_salary_after_6_months).to.eql(Number(reqData.salary) * 2);
    });

#### 16. Check that the qa_salary_after_12_months parameter is equal to salary*2.7 from request (pick salary from request)

    pm.test("Check 12MonthSalary", function () {
        pm.expect(respData.qa_salary_after_12_months).to.eql(reqData.salary * 2.7);
    });

#### 17. Check that the parameter qa_salary_after_1.5_year is equal to salary*3.3 from request (salary pick up from request)

    pm.test("Check 1.5_yearSalary", function () {
        pm.expect(respData["qa_salary_after_1.5_year"]).to.eql(reqData.salary * 3.3);
    });

#### 18. Check that the qa_salary_after_3.5_years parameter is equal to salary*3.8 from request (pick salary from request)

    pm.test("Check 3.5_yearSalary", function () {
        pm.expect(respData["qa_salary_after_3.5_years"]).to.eql(reqData.salary * 3.8);
    });

#### 19. Check that in the person parameter, [1] element from u_name is equal to salary from request (pick salary from request)

    pm.test("Check u_name element with salary", function () {
        pm.expect(respData.person.u_name[1]).to.eql(+reqData.salary);
    });

#### 20. Check that the u_age parameter is equal to age from request (age is taken from request)

    pm.test("Check ages", function (){
        pm.expect(respData.person.u_age).to.eql(+reqData.age)
    })

#### 21. Check that the u_salary_5_years parameter is equal to salary*4.2 from request (pick salary from request)

    pm.test("Check 5 years salary", function(){
        pm.expect(respData.person.u_salary_5_years).to.eql(reqData.salary * 4.2)
    })

#### 22. ***Write a loop that will output the list items from the person parameter to the console in order

    for (i in respData.person){
        console.log(`${i} = ${respData.person[i]}`)
    }
