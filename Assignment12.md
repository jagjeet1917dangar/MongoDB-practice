Task 1: Add more students to the students collection

db.students.insertMany([
  { name: "Aditi Sharma", rollNumber: "CS1006", courses: ["MATH101", "CS101"] },
  { name: "Raj Malhotra", rollNumber: "CS1007", courses: ["PHY101", "CS101"] },
  { name: "Neha Singh", rollNumber: "CS1008", courses: ["MATH101", "ENG101"] },
  { name: "Karan Verma", rollNumber: "CS1009", courses: ["CS101", "HIST101"] },
  { name: "Pooja Desai", rollNumber: "CS1010", courses: ["MATH101", "CS101", "PHY101"] }
]);

Task 2: Insert a new course into the courses collection

db.courses.insertOne({
  courseCode: "CS202",
  name: "Data Structures",
  credits: 3,
  instructor: "Prof. Krishna"
});

Task 3: Fetch a specific student's record by roll number

db.students.find({ rollNumber: "CS1002" });

Task 4: Query all students who are enrolled in a particular course

db.students.find({ courses: "MATH101" });

Task 5: Update a student's courses

db.students.updateOne(
  { rollNumber: "CS1001" },
  { $addToSet: { courses: "CS202" } }
);

Task 6: Remove a course from a student's courses list

db.students.updateOne(
  { name: "Mahir" },
  { $pull: { courses: "MATH101" } }
);

Task 7: Find all courses with 3 credits

db.courses.find({ credits: 3 });

Task 8: Find students who have enrolled in more than 2 courses

db.students.find({ courses: { $size: { $gt: 2 } } });

Task 9: Use the $in operator to find students enrolled in multiple courses

db.students.find({ courses: { $in: ["CS101", "MATH202"] } });

Task 10: Fetch all students from a specific department (e.g., CSE)

db.students.find({ department: "CSE" });

Task 11: Query students who are in their 3rd year

db.students.find({ year: 3 });

Task 12: Query students using a range for their year

db.students.find({ year: { $gte: 2, $lte: 3 } });

Task 13: Count the total number of students in each department

db.students.aggregate([
  { $group: { _id: "$department", totalStudents: { $sum: 1 } } }
]);

Task 14: Group courses by credits

db.courses.aggregate([
  { $group: { _id: "$credits", totalCourses: { $sum: 1 } } }
]);

Task 15: Find the highest credit course

db.courses.find().sort({ credits: -1 }).limit(1);
