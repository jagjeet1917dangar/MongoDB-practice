// 1. Additional Questions on CRUD Operations
// Insert new students into the "students" collection with random data:

db.students.insertMany([
  { rollNumber: 101, name: "John Doe", department: "CS", courses: ["CS101", "MATH101"], year: 2023 },
  { rollNumber: 102, name: "Jane Smith", department: "ECE", courses: ["ECE101", "PHYS101"], year: 2022 },
  { rollNumber: 103, name: "Sam Wilson", department: "ME", courses: ["ME101", "CHEM101"], year: 2024 },
  { rollNumber: 104, name: "Anna Brown", department: "CS", courses: ["CS102"], year: 2023 },
]);


// Update the department of a student based on their roll number:

db.students.updateOne(
  { rollNumber: 101 },
  { $set: { department: "IT" } }
);

// Remove all students who have enrolled in less than 3 courses:

db.students.deleteMany(
  { "courses.2": { $exists: false } }
);


// 2. Aggregation Exercise

// Find the department with the most number of students: 
// ANS -
db.students.aggregate([
  { $group: { _id: "$department", studentCount: { $sum: 1 } } },
  { $sort: { studentCount: -1 } },
  { $limit: 1 },
]);

// 3. Advanced Querying Exercise

// Query students who have enrolled in a specific set of courses (e.g., CS101 and MATH101):
// ANS - 
db.students.find({
  courses: { $all: ["CS101", "MATH101"] }
});

// Measure query performance using explain():
// ANS - 
db.students.find({ department: "CS" }).explain("executionStats");



