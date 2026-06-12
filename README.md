# school-erp
erDiagram

    USERS {
        ObjectId _id PK
        string name
        string email
        string password
        string role
        string phone
        date createdAt
    }

    DEPARTMENTS {
        ObjectId _id PK
        string name
        string code
        ObjectId deanId FK
        string description
        date createdAt
    }

    CLASSES {
        ObjectId _id PK
        string name
        string section
        ObjectId departmentId FK
        ObjectId mentorId FK
        int year
        string semester
    }

    SUBJECTS {
        ObjectId _id PK
        string name
        string code
        ObjectId classId FK
        ObjectId teacherId FK
        int totalCredits
        string semester
    }

    STUDENTS {
        ObjectId _id PK
        ObjectId userId FK
        string rollNumber
        ObjectId classId FK
        ObjectId departmentId FK
        ObjectId mentorId FK
        string feeStatus
        date admissionDate
        string address
        string guardianName
        string guardianPhone
    }

    TEACHERS {
        ObjectId _id PK
        ObjectId userId FK
        string employeeId
        ObjectId departmentId FK
        string qualification
        string specialization
        date joiningDate
    }

    MENTORS {
        ObjectId _id PK
        ObjectId userId FK
        string employeeId
        ObjectId departmentId FK
        ObjectId classId FK
        string qualification
    }

    ATTENDANCE {
        ObjectId _id PK
        ObjectId studentId FK
        ObjectId subjectId FK
        ObjectId markedById FK
        date date
        string status
        string remarks
    }

    RESULTS {
        ObjectId _id PK
        ObjectId studentId FK
        ObjectId subjectId FK
        ObjectId createdById FK
        string examType
        float marksObtained
        float totalMarks
        string grade
        string semester
        date examDate
    }

    ASSIGNMENTS {
        ObjectId _id PK
        ObjectId subjectId FK
        ObjectId createdById FK
        string title
        string description
        date dueDate
        float totalMarks
        string status
    }

    SUBMISSIONS {
        ObjectId _id PK
        ObjectId assignmentId FK
        ObjectId studentId FK
        string fileUrl
        date submittedAt
        float marksAwarded
        string feedback
        string status
    }

    FEES {
        ObjectId _id PK
        ObjectId studentId FK
        string feeType
        float amount
        date dueDate
        date paidDate
        string status
        string transactionId
        string semester
    }

    ANNOUNCEMENTS {
        ObjectId _id PK
        ObjectId createdById FK
        string title
        string content
        string targetRole
        ObjectId targetClassId FK
        date createdAt
        boolean isActive
    }

    MENTOR_NOTES {
        ObjectId _id PK
        ObjectId mentorId FK
        ObjectId studentId FK
        string note
        string type
        date createdAt
        boolean isPrivate
    }

    TIMETABLE {
        ObjectId _id PK
        ObjectId classId FK
        ObjectId subjectId FK
        ObjectId teacherId FK
        string dayOfWeek
        string startTime
        string endTime
        string room
    }

    LEAVE_REQUESTS {
        ObjectId _id PK
        ObjectId studentId FK
        ObjectId approvedById FK
        string reason
        date fromDate
        date toDate
        string status
        date appliedAt
    }

    USERS ||--o| STUDENTS : "is a"
    USERS ||--o| TEACHERS : "is a"
    USERS ||--o| MENTORS : "is a"

    DEPARTMENTS ||--o{ CLASSES : "has"
    DEPARTMENTS ||--o{ TEACHERS : "belongs to"
    DEPARTMENTS ||--o{ MENTORS : "belongs to"
    DEPARTMENTS ||--o{ STUDENTS : "enrolled in"

    USERS ||--o{ DEPARTMENTS : "dean manages"

    CLASSES ||--o{ STUDENTS : "contains"
    CLASSES ||--o{ SUBJECTS : "has"
    CLASSES ||--o{ TIMETABLE : "scheduled in"
    CLASSES ||--|| MENTORS : "assigned to"

    SUBJECTS ||--o{ ATTENDANCE : "tracked for"
    SUBJECTS ||--o{ RESULTS : "graded in"
    SUBJECTS ||--o{ ASSIGNMENTS : "has"
    SUBJECTS ||--o{ TIMETABLE : "appears in"

    STUDENTS ||--o{ ATTENDANCE : "has"
    STUDENTS ||--o{ RESULTS : "receives"
    STUDENTS ||--o{ SUBMISSIONS : "submits"
    STUDENTS ||--o{ FEES : "pays"
    STUDENTS ||--o{ MENTOR_NOTES : "noted in"
    STUDENTS ||--o{ LEAVE_REQUESTS : "applies for"

    ASSIGNMENTS ||--o{ SUBMISSIONS : "receives"

    USERS ||--o{ ANNOUNCEMENTS : "creates"
    USERS ||--o{ RESULTS : "enters"
    USERS ||--o{ ATTENDANCE : "marks"

    MENTORS ||--o{ MENTOR_NOTES : "writes"
    MENTORS ||--o{ LEAVE_REQUESTS : "approves"
