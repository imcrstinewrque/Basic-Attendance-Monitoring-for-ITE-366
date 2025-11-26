# BASIC ATTENDANCE MONITORING SYSTEM FOR ITE 366


students = {
    "S001": "John Santos",
    "S002": "Maria Reyes", 
    "S003": "Carlos Lim",
    "S004": "Anna Torres",
    "S005": "Mike Cruz"
}
attendance_records = {}

def teacher_login():
    print("\n--- TEACHER LOGIN ---")
    username = input("Username: ")
    password = input("Password: ")
    
    if username == "teacher" and password == "ite366":
        teacher_dashboard()
    else:
        print("Invalid login!")
        main()

def teacher_dashboard():
    while True:
        print("\n--- TEACHER DASHBOARD ---")
        print("1. Mark Attendance")
        print("2. View All Records") 
        print("3. Generate Report")
        print("4. Logout")
        
        choice = input("Choose: ")
        
        if choice == "1":
            mark_attendance()
        elif choice == "2":
            view_all_records()
        elif choice == "3":
            generate_report()
        elif choice == "4":
            break
        else:
            print("Invalid choice!")

def mark_attendance():
    print("\n--- MARK ATTENDANCE ---")
    date = input("Enter date (MM/DD): ")
    attendance_records[date] = {}
    
    present_count = 0
    absent_count = 0
    
    for sid, name in students.items():
        print(f"\n{name}:")
        print("P - Present, A - Absent, L - Late")
        status = input("Status: ").upper()
        
        if status == "P":
            attendance_records[date][sid] = "Present"
            present_count += 1
        elif status == "A":
            attendance_records[date][sid] = "Absent" 
            absent_count += 1
        elif status == "L":
            attendance_records[date][sid] = "Late"
            present_count += 1
        else:
            attendance_records[date][sid] = "Absent"
            absent_count += 1
    
    print(f"\nAttendance saved for {date}!")
    print(f"Present: {present_count}, Absent: {absent_count}")

def view_all_records():
    print("\n--- ALL ATTENDANCE RECORDS ---")
    if not attendance_records:
        print("No records found.")
        return
    
    for date, records in attendance_records.items():
        present = sum(1 for status in records.values() if status in ["Present", "Late"])
        absent = len(students) - present
        print(f"\n{date}: Present: {present}, Absent: {absent}")
        for sid, status in records.items():
            print(f"  {students[sid]}: {status}")

def generate_report():
    print("\n--- GENERATE REPORT ---")
    if not attendance_records:
        print("No data available.")
        return
    
    print("ATTENDANCE SUMMARY REPORT")
    print("=" * 30)
    
    for date in attendance_records:
        present = sum(1 for status in attendance_records[date].values() if status in ["Present", "Late"])
        absent = len(students) - present
        print(f"\n{date}: {present} present, {absent} absent")

def student_login():
    print("\n--- STUDENT LOGIN ---")
    sid = input("Student ID: ")
    
    if sid in students:
        student_dashboard(sid)
    else:
        print("Student not found!")
        main()

def student_dashboard(sid):
    print(f"\n--- WELCOME {students[sid]} ---")
    
    while True:
        print("\n1. View My Attendance")
        print("2. Logout")
        
        choice = input("Choose: ")
        
        if choice == "1":
            view_my_attendance(sid)
        elif choice == "2":
            break
        else:
            print("Invalid choice!")

def view_my_attendance(sid):
    print(f"\n--- MY ATTENDANCE RECORD ---")
    
    if not attendance_records:
        print("No attendance records.")
        return
    
    total_classes = 0
    present_count = 0
    
    for date, records in attendance_records.items():
        if sid in records:
            total_classes += 1
            status = records[sid]
            print(f"{date}: {status}")
            if status in ["Present", "Late"]:
                present_count += 1
    
    if total_classes > 0:
        print(f"\nSummary: {present_count}/{total_classes} classes attended")

def main():
    print("=== BASIC ATTENDANCE MONITORING SYSTEM ===")
    print("              ITE 366 CLASS")
    
    while True:
        print("\n1. Teacher Login")
        print("2. Student Login")
        print("3. Exit System")
        
        choice = input("Choose: ")
        
        if choice == "1":
            teacher_login()
        elif choice == "2":
            student_login()
        elif choice == "3":
            print("Thank you for using the system!")
            break
        else:
            print("Invalid choice!")

# Run the system
if __name__ == "__main__":
    main()
