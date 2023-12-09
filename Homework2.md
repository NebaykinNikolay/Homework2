class Student:
  def __init__(self, name, surname, gender):
      self.name = name
      self.surname = surname
      self.gender = gender
      self.finished_courses = []
      self.courses_in_progress = []
      self.grades = {}
      self.evaluates_lectures = []  
  def rate_lecturer(self, lecturer, course, grade):
      if isinstance(lecturer, Lecturer) and course in self.evaluates_lectures and course in lecturer.teaches_the_course:
          if course in lecturer.grades:
              lecturer.grades[course] += [grade]
          else:
              lecturer.grades[course] = [grade]
      else:
          return 'Ошибка'

  def set_evaluates_lectures(self, courses):
    self.evaluates_lectures = courses

class Mentor:
  def __init__(self, name, surname):
      self.name = name
      self.surname = surname
      self.courses_attached = []
      


class Lecturer(Mentor):
   def __init__(self, name, surname):  
      super().__init__(name, surname)
      self.teaches_the_course = []
      self.grades = {} 

class Rewiewer(Mentor):
        def rate_hw(self, student, course, grade):
          if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
              if course in student.grades:
                  student.grades[course] += [grade]
              else:
                  student.grades[course] = [grade]
          else:
              return 'Ошибка'


best_student = Student('Roy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']
best_student.set_evaluates_lectures(['Python'])

cool_mentor = Rewiewer('Victor', 'Ivanov')
cool_mentor.courses_attached += ['Python']

good_mentor_l = Lecturer('Ivan', 'Vasilyev')
good_mentor_l.teaches_the_course += ['Python']

cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)
best_student.rate_lecturer(good_mentor_l, 'Python', 10)
print(best_student.grades)
print(good_mentor_l.grades)
