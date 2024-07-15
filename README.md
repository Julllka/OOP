# OOP

class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname


class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}
        self.courses_attached = []

    def __dict__(self):
        dict = {'Python': [3, 5],
              'Java': [2, 10],
              'Git': [6, 9],
              'Введение в программирование': [8, 7]
              }
    def __str__(self):
        return f'Имя: {self.name}\n'
        f"Фамилия: {self.surname}\n"
        f"Средняя оценка за лекции: {self.grades()}\n"

    def __lt__(self, other):
        return self.grades < other.grades

class Reviewer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.courses_attached = []


    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

    def __str__(self):
        return f'Имя: {self.name}\n'
        f"Фамилия: {self.surname}\n"


class Student:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_in_progress = []
        self.grades = {}
        self.finished_courses = []
        self.courses_attached = []

    def rate_lw(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and course in self.courses_attached and course in lecturer.courses_in_progress:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'

    def __str__(self):
        return f'Имя: {self.name}\n'
        f"Фамилия: {self.surname}\n"
        f"Средняя оценка за домашние задания: {self.grades()}\n"
        f"Курсы в процессе изучения: {", ".join(self.courses_in_progress)}\n"
        f"Завершенные курсы: {", ".join(self.finished_courses)}"

    def __lt__(self, other):
        return self.grades < other.grades


#student_list = [student, student_1, student_2, student_3]
#lecturer_list = [lecturer, lecturer_1, lecturer_2, lecturer_3]
#reviewer_list = [reviewer, reviewer_1]


lecturer = Lecturer('Some', 'Buddy')
lecturer.courses_attached += ['Python', 'Java', 'Введение в программирование', 'Git']
lecturer_1 = Lecturer('Ivan', 'Ivanov')
lecturer_1.courses_attached += ['Git', 'Введение в программирование']
lecturer_2 = Lecturer('Petr', 'Petrov')
lecturer_2.courses_attached += ['Java']
lecturer_3 = Lecturer('Semen', 'Zarev')
lecturer_3.courses_attached += ['Введение в программирование']



student = Student('Ruoy', 'Eman')
student.courses_in_progress += ['Python']
student_1 = Student('Denis', 'Sviridov')
student_1.courses_in_progress += ['Python']
student_2 = Student('Sonia', 'Moskvina')
student_2.courses_in_progress += ['Java']
student_3 = Student('Sidor', 'Petrov')
student_3.finished_courses += ['Введение в программирование']

student.rate_lw(lecturer, 'Python', 5)
student_1.rate_lw(lecturer, 'Python', 10)
student_2.rate_lw(lecturer_2, 'Java', 10)
student_3.rate_lw(lecturer_3, 'Python', 6)




reviewer = Reviewer('Sume', 'Buddy')
reviewer.courses_attached += ['Python']
reviewer_1 = Reviewer('Stepan', 'Ivanov')
reviewer_1.courses_attached += ['Java']


reviewer.rate_hw(student, 'Java', 8)
reviewer_1.rate_hw(student_2, 'Java', 7)
reviewer.rate_hw(student_2, 'Java', 9)
reviewer_1.rate_hw(student_3, 'Python', 8)
reviewer.rate_hw(student_3, 'Python', 7)
