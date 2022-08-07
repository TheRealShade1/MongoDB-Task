## 1. Create database named: FacultySystemDB.

use FacultySystemDB;

## 2. Create collection (student) that has:

•FirstName: string

•LastName: string

•Age: Number

•Faculty: An object that has Name and Address

•Grades: An array of objects, each object has: CourseName, Grade, Pass (Boolean).

•IsFired: Boolean

 
 db.createCollection("student", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         properties: {
            FirstName: {
               bsonType: "string"
            },
            LastName: {
               bsonType: "string"
            },
            Age: {
               bsonType: "int",
               minimum: 15,
               maximum: 100,
            },
            Faculty: {
                  bsonType: "object",
                  properties: {
                     FacultyName: {
                        bsonType: "string"
                     },
                     FacultyAddress: {
                        bsonType: "string"
                     }                     
                  }
            },
            Grades: {
               bsonType: ["array"],
               items: {
                  bsonType: "object",
                  required: ["CourseName", "Grade", "Pass"],
                  properties: {
                     CourseName: {
                        bsonType: "string"
                     },
                     Grade: {
                        bsonType: "string"
                     },
                     Pass: {
                        bsonType: "bool"
                     }
                  }
               }
            },

            IsFired: {
               bsonType: "bool"
            },
            }
         }
      }
   }
)
