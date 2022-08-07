# MongoDB Queries:

## 1. Create database named: FacultySystemDB.

    use FacultySystemDB;

## 2. Create collection (student) that has:

    db.createCollection("student",{
     validator: {
      $jsonSchema: {
         bsonType: "object",
         properties: {
            FirstName: {bsonType: "string"},
            LastName: {bsonType: "string"},
            Age:{bsonType:"int"},
            Faculty:{
                bsonType:"object",
                properties:{
                    Name:{bsonType:"string"},
                    Address:{bsonType:"string"}
                }
            },
            Grades:{
                bsonType:"array",
                items:{
                    bsonType: "object",
                    properties:{
                        CourseName:{bsonType:"string"},
                        Grade:{bsonType:"int"},
                        Pass:{bsonType:"bool"},
                        
                    }
                }
            },
            IsFired:{bsonType:"bool"}
           }
         }
       }
     });

## 3. Insert 3 (at least) documents in Student collection with different values.

•Try inserting one record each time

    db.student.insertOne({
     FirstName: "omar",
     LastName: "adel",
     Age: 22,
     Faculty:{
         Name:"Computer science",
         Address:"Helwan university"
     },
     Grades:[
         {
             CourseName:"Database",
             Grade: 100,
             Pass:true
         },{
             CourseName:"Object oriented Programming",
             Grade: 100,
             Pass:true
         }
     ],
      IsFired:false 
      
    });


    db.student.insertOne({
     FirstName: "ahmed",
     LastName: "adel",
     Age: 20,
     Faculty:{
         Name:"Computer science",
         Address:"Helwan university"
     },
     Grades:[
         {
             CourseName:"Database",
             Grade: 87,
             Pass:true
         },{
             CourseName:"Object oriented Programming",
             Grade: 85,
             Pass:true
         }
     ],
    IsFired:false 
    
    });
    
    
    db.student.insertOne({
     FirstName: "mahmoud",
     LastName: "karim",
     Age: 24,
     Faculty:{
         Name:"Computer science",
         Address:"Helwan university"
     },
     Grades:[
         {
             CourseName:"Database",
             Grade: 80,
             Pass:true
         },{
             CourseName:"Object oriented Programming",
             Grade: 90,
             Pass:true
         }
     ],
    IsFired:false 
    
    });
    
•Try inserting collection using one insert statement.

    db.student.insertMany([
      {
        FirstName: ",mohamed",
        LastName: "samy",
        Age: 22,
        Faculty:{
            Name:"Computer science",
            Address:"cairo university"
        },
        Grades:[
            {
                CourseName:"Database",
                Grade: 77,
                Pass:true
            },{
                CourseName:"Object oriented Programming",
                Grade: 60,
                Pass:true
            }
        ],
        IsFired:false
    },
    {
        FirstName: "may",
        LastName: "mahmoud",
        Age: 22,
        Faculty:{
            Name:"science and medicine",
            Address:"Ain Shams university"
        },
        Grades:[
            {
                CourseName:"medicine",
                Grade: 84,
                Pass:true
            },{
                CourseName:"Toxicology",
                Grade: 70,
                Pass:true
            }
        ],
        IsFired:false
    },
    {
        FirstName: "fatma",
        LastName: "allam",
        Age: 22,
        Faculty:{
            Name:"Computer science",
            Address:"Helwan university"
        },
        Grades:[
            {
                CourseName:"compiler",
                Grade: 70,
                Pass:true
            },{
                CourseName:"computer organization",
                Grade: 40,
                Pass:false
            }
        ],
        IsFired:false
       }
    ]);
    
## 4.Retrieve the following data:
    
•All Students.

	db.student.find({});

•Student with specific First Name.

	db.student.find({FirstName:"ahmed"});

•Students who his First Name=Ahmed, or Last Name= Ahmed.

	db.student.find({FirstName:"Ahmed",LastName:"Ahmed"});

•Students that their First name isn't "Ahmed".

	db.student.find({FirstName:{$ne:"Ahmed"}});

•Students with Age less than 21.

	db.student.find({Age:{$lt:21}});

•All fired students.

	db.student.find({IsFired:true});

•Students with Age more than or equal to 21, and their faculty isn't NULL.
	
	db.student.find({
   	    $and:[
                {Age:{$gte:21}},{Faculty:{$ne:null}}
   	    ]
	});
		
•Display student with specific First Name, and display his First Name, Last name, IsFired fields only.

	db.student.find({FirstName:"ahmed"},{FirstName:1,LastName:1,IsFired:1,_id:0});
 
## 5.Update the student with specific FirstName, and change his LastName.

•Try Update() statement.

	db.student.update({FirstName:"ahmed"},{$set:{LastName:"ahmed"}});

•Try Update() with Mulit option.

	db.student.updateOne({FirstName:"ahmed"},{$set:{LastName:"ahmed"}},{upsert:true});

•Try Save().

	db.student.save({FirstName:"Omar",LastName:"akram"});

## 6.Delete Fired students.
	
	db.student.deleteMany({IsFired:true});

## 7.Delete all students collection.
	
	db.student.deleteMany({});	

## 8.Delete the whole DB.

	db.dropDatabase();		

## 9.Create new database named: FacultySystemV2.

	use FacultySystemV2;

•Create student collection that has (FirstName, lastName, IsFired, FacultyID, array of objects, each object has CourseID, grade).

    db.createCollection("student",{
      validator: {
          $jsonSchema: {
              bsonType: "object",
              properties: {
                  FirstName: {bsonType: "string"},
                  LastName: {bsonType: "string"},
                  IsFired:{bsonType:"bool"},
                  FacultyID:{bsonType:"objectId"},
                  Grades:{
                      bsonType:"array",
                      items:{
                          bsonType: "object",
                          properties:{
                              CourseID:{bsonType:"objectId"},
                              grade:{bsonType:"int"},
                           }
                       }
                   },           
               } 
           }
        }
     });

•Create Faculty collection that has (Faculty Name, Address).

     db.createCollection("Faculty ",{
          validator: {
             $jsonSchema: {
                bsonType: "object",
                properties: {
                    Name: {bsonType: "string"},
                    Address: {bsonType: "string"},  
                 } 
             }
         }
     });

•Create Course collection, which has (Course Name, Final Mark).

    db.createCollection("Course",{
         validator: {
            $jsonSchema: {
                bsonType: "object",
                properties: {
                    CourseName: {bsonType: "string"},
                    FinalMark: {bsonType: "string"},  
                } 
            }
        }
    });
