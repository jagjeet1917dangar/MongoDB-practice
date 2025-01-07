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

Task 16: Use the $and operator for filtering students

db.students.find({
  $and: [
    { department: "CSE" },
    { courses: { $exists: true, $size: { $gt: 2 } } }
  ]
});

Task 17: Add a new field activeStatus set to true

db.students.updateMany({}, { $set: { activeStatus: true } });

Task 18: Rename coursesEnrolled to enrolledCourses

db.students.updateMany({}, { $rename: { "coursesEnrolled": "enrolledCourses" } });

Task 19: Add a field graduationYear with a default value

db.students.updateMany({}, { $set: { graduationYear: 2025 } });

Task 20: Add course CS303 to Mahir’s coursesEnrolled

db.students.updateOne(
  { name: "Mahir" },
  { $push: { coursesEnrolled: "CS303" } }
);

Task 21: Remove course CS101 from Jenil’s courses

db.students.updateOne(
  { name: "Jenil" },
  { $pull: { courses: "CS101" } }
);

Task 22: Remove student with roll number CS1004

db.students.deleteOne({ rollNumber: "CS1004" });

Task 23: Find students enrolled in both CS101 and MATH202

db.students.find({ courses: { $all: ["CS101", "MATH202"] } });

Task 24: Search for students whose name starts with "A"

db.students.find({ name: { $regex: "^A", $options: "i" } });

Task 25: Find students with an entry in coursesEnrolled

db.students.find({ coursesEnrolled: { $exists: true, $not: { $size: 0 } } });

Task 26: Add a grades field

db.students.updateMany({}, { $set: { grades: [] } });

Task 27: Use $elemMatch to find specific courses and grades

db.students.find({
  grades: { $elemMatch: { course: "CS101", grade: "A" } }
});

Task 28: Query students with exactly 2 courses enrolled

db.students.find({ coursesEnrolled: { $size: 2 } });

Task 29: Perform text search for "Digital Electronics"

db.courses.createIndex({ title: "text" });

Task 30: Create a compound index on department and year

db.students.createIndex({ department: 1, year: 1 });

Task 31: Sort students by rollNumber

db.students.find().sort({ rollNumber: 1 });

Task 32: Create a unique index on rollNumber

db.students.createIndex({ rollNumber: 1 }, { unique: true });

Task 33: Update course CS101 to Intro to Programming

db.courses.updateOne(
  { courseCode: "CS101" },
  { $set: { name: "Intro to Programming" } }
);

Task 34: Backup the database

mongodump --db CodingGitaStudents --out /path/to/backup

Task 35: Restore the database

mongorestore --db CodingGitaStudents /path/to/backup/CodingGitaStudents

Task 36: Use $project to reshape data

db.students.aggregate([
  { $project: { name: 1, department: 1, _id: 0 } }
]);

Task 37: Use $unwind to split coursesEnrolled

db.students.aggregate([
  { $unwind: "$coursesEnrolled" }
]);

Task 38: Limit to the first 3 students

db.students.find().limit(3);

Task 39: Skip the first 2 students

db.students.find().skip(2);

Task 40: Use $lookup to join students with courses

db.students.aggregate([
  {
    $lookup: {
      from: "courses",
      localField: "coursesEnrolled",
      foreignField: "courseCode",
      as: "courseDetails"
    }
  }
]);

Task 41: Create a studentFeedback collection

db.studentFeedback.insertOne({
  studentRollNumber: "CS1001",
  feedbackText: "Great course content!",
  date: new Date()
});

Task 42: Find feedback from Jenil

db.studentFeedback.find({ studentRollNumber: "CS1002" });

Task 43: Update multiple fields for Arjun

db.students.updateOne(
  { name: "Arjun" },
  { $set: { department: "ECE", coursesEnrolled: ["CS202", "CS303"] } }
);

Task 44: Create an index on coursesEnrolled

db.students.createIndex({ coursesEnrolled: 1 });

Task 45: Query for nested grades

db.students.find({
  grades: { $elemMatch: { course: "CS101", grade: "A" } }
});

