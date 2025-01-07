Task 1: Add multiple students
Insert at least 5 students into the students collection with unique roll numbers, names, departments, years, and subjects enrolled.
Ans:

db.createCollection("students");

db.students.insertMany([
  { 
    "name": "Jenil",
    "rollNumber": 101,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB"]
  },
  { 
    "name": "Mahir",
    "rollNumber": 102,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },
  { 
    "name": "Arjun",
    "rollNumber": 103,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  },
]);

db.students.insertMany([
  { 
    "name": "krutgaya",
    "rollNumber": 104,
    "department": "Macanical",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB"]
  },
  { 
    "name": "jatan",
    "rollNumber": 105,
    "department": "Ec",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },
  { 
    "name": "jenil",
    "rollNumber": 106,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  }
]);


Task 2: Add multiple subjects
Insert 4 subjects into the subjects collection, each with 3 to 5 topics.

Ans:

db.createCollection("subjects");

db.subjects.insertMany([{ 
    "subjectName": "React",
    "topics": [
      "JSX", 
      "Components", 
      "State", 
      "Props", 
      "Hooks"
    ]
  },
  { 
    "subjectName": "NodeJS", 
    "topics": [
      "Modules", 
      "Express", 
      "File System", 
      "Asynchronous Programming"
    ]
  },
  { 
    "subjectName": "MongoDB", 
    "topics": [
      "Database Design", 
      "CRUD Operations", 
      "Aggregation", 
      "Indexes"
    ]
  },
  { 
    "subjectName": "React",
    "topics": [
      "JSX", 
      "Components", 
      "State", 
      "Props", 
      "Hooks"
    ]
  },
  { 
    "subjectName": "NodeJS", 
    "topics": [
      "Modules", 
      "Express", 
      "File System", 
      "Asynchronous Programming"
    ]
  },
  { 
    "subjectName": "HTML", 
    "topics": [
      "Forms", 
      "Padding", 
      "Margin", 
      "Heading"
    ]
  }]);


Task 3: Query students based on subject enrollment
Query the students collection to find all students who are enrolled in NodeJS.

Ans:  db.students.find({"subjectsEnrolled":"NodeJS"});

Task 4: Add a new topic to a subject
Add a new topic to the NodeJS subject.

Ans: db.subjects.updateOne({"subjectName": "NodeJS"},{$push: {"topics":"program"}});

Task 5: Query subjects with multiple topics
Query the subjects collection to find subjects that contain at least 4 topics.

Ans: db.subjects.find({topics: { $size: 4 }});

Task 6: Update student enrollment
Add the subject "React Native" to Jenil's subjects.

Ans: db.students.updateOne({"name":"jenil"},{$push:{"subjectsEnrolled":"React Native"}});

Task 7: Query all students
Query all students in the database and print out their names and enrolled subjects.

Ans: db.students.find({},{name:1,subjectsEnrolled:1});
<!-- here {} is represent all data in collection -->

Task 8: Update multiple students' year
Update the year for all students in the Computer Science department to year 3.

Ans:   db.students.updateMany({'department': 'Computer Science'},{$set: {"year":3}});

Task 9: Add new topics to multiple subjects
Add new topics to React, NodeJS, and MongoDB subjects. Ensure each subject gets at least one new topic.

Ans:  
db.subjects.updateOne({ name: "React" }, { $push: { topics: "New React Topic" }});
db.subjects.updateOne({ name: "NodeJS" }, { $push: { topics: "New React Topic" }});
db.subjects.updateOne({ name: "MongoDB" }, { $push: { topics: "New React Topic" }});

Task 10: Remove a topic from a subject
Remove the topic "Express" from the NodeJS subject.

Ans: db.subjects.updateOne({ name: "NodeJS" },{ $pull: { topics: "Express" }});
<!-- pull for delete one element -->

Task 11: Query all students in a specific year
Query and return all students in year 2 or year 3.

Ans:  db.students.find({$or: [{'year':2},{'year':3}]});

Task 12: Delete a student by roll number
Delete a student from the database using their roll number.

Ans:  db.students.deleteOne({"rollnumber":105});

Task 13: Delete all students from a department
Delete all students who belong to the Electrical Engineering department.

Ans: db.students.deleteOne({"department":"Electrical Engineering"});

Task 14: Retrieve all topics for a subject
Query the MongoDB subject and retrieve all topics listed for it.

Ans: db.subjects.find({"subjectName":"MongoDB"},{"topics":1});


Task 15: Count the number of subjects in which a student is enrolled
Write a query that returns the number of subjects each student is enrolled in.

Ans: db.students.aggregate([
  {
    $project: {
      name: 1, // Include the student's name
      numberOfSubjects: { $size: "$subjectsEnrolled" } // Calculate the size of the enrolledSubjects array
    }
  }
]);