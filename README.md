
//41 / 66666666666666666666666666666666666666666666666666666666666

// proj 2

(* The focus of this problem is on courses and curricula at DTU. A course is uniquely identified
by a course number and a course is described by a title and a number of ECTS point. The
course base is a map from course numbers to course descriptions. *)

type CourseNo = int;; type Title = string;; type ECTS = int;; //type declarations
type CourseDesc = Title * ECTS;; type CourseBase = Map<CourseNo, CourseDesc>;;

(* We require in this problem that valid ECTS points are positive integers that are divisible
by 5, that is, 5, 10, 15, 20, ... is the sequence of valid ECTS points. *)

(* 1. Declare a function isValidCourseDesc: CourseDesc -> bool,
where isValidCourseDesc desc is true if the ECTS part of desc is valid.*)

let CourseDesc = Map.ofList [("a1",25); ("a2",4); ("a3",5)];;

// modulo function to set fitting ects values to zero
let CourseDesc0 CourseDesc = Map.map (fun _ ects -> ects % 5) CourseDesc;;

// checker if all values are zero
let isValidCourseDesc CourseDesc = Map.forall (fun _ ects -> ects = 0) (CourseDesc0 CourseDesc);;

// call function
isValidCourseDesc CourseDesc;;

(* 2. Declare a function isValidCourseBase: CourseBase -> bool,
where isValidCourseBase cb is true if every course description occurring the course
base cb is valid, that is, it satisfies the predicate isValidCourseDesc. *)

// similar procedure to q. 1
let CourseBase = Map.ofList [(0,("a1",25)); (1,("a2",4)); (2,("a3",5))];;

// exctracting CourseDesc from CourseBase, then modulo 5
let CourseBase0 CourseBase = Map.map (fun _ (_,ects) -> ects % 5) CourseBase;;

// boolean check
let isValidCourseBase CourseBase = Map.forall (fun _ ects -> ects = 0) (CourseBase0 CourseBase);;

isValidCourseBase CourseBase;;
