##PROG101_Esther-Aminata_-Jabasandy

ssignment Focus: PROG101 Individual Assignment 1 ("Designing Logical Solutions for Sierra Leone Community Challenges") at Limkokwing University.   Core Objective: Design a complete, menu-driven logical system called CHC-Triage to solve unsafe waiting times and lack of prioritization at community health centres in Sierra Leone.   

##OverviewProject Name: 
(Community Health Centre Patient Triage and Queue Management System).   Course: PROG101 – Principles of Programming Logic and Design.   Institution: Limkokwing University of Creative Technology, Sierra Leone.   System Summary: CHC-Triage is a menu-driven logical system designed for community health clinics. It handles 5 primary options: registering a patient, calling the next patient, displaying queue status, generating daily reports, and exiting. It uses clear, fixed rules (such as age, temperature, pain score, and danger signs) to categorize patients into Emergency, Urgent, or Routine queues to ensure that the sickest individuals are treated 

The United Nations Sustainable Development Goals (SDGs):   

##SDG 3: Good Health and Well-being – Supports Target 3.1 (reducing maternal mortality), Target 3.2 (ending preventable deaths of newborns and children under five), and Target 3.8 (access to quality essential health services).   SDG 10: Reduced Inequalities – Ensures every patient is evaluated using identical medical rules rather than social standing or arrival order.   SDG 9: Industry, Innovation and Infrastructure – Supports Target 9.c by promoting information and communication technology access in underserved communities.   


##Problem DescriptionThe Core Issue: Many Community Health Centres (CHCs) and peripheral health units in Sierra Leone register patients strictly on a first-come, first-served basis. Consequently, high-risk patients (such as a child with a high fever or a bleeding pregnant person) may wait on the same bench as someone with a mild illness, relying solely on the memory and judgment of an overworked nurse.   Who is Affected: Patients (especially children under five, pregnant women, and the elderly), nurses, community health officers, and families traveling long distances.

##SolutionLogical Design & Workflow: 
The system runs as a menu-based loop. During registration, it validates patient inputs (such as age, temperature, pain score, pregnancy status, and danger signs) and computes a priority score.   Queue Management & Fairness:Maintains three separate queues (Emergency, Urgent, and Routine), always serving Emergency first.

3. Pseudocode
The pseudocode below shows the input, processing and output of the whole system. Words in capital letters are keywords, and text after // is a comment.
1. Constants, Data Types and Variables
CONSTANT URGENT_THRESHOLD = 5            // INTEGER: score at which a patient becomes URGENT
CONSTANT PROMOTE_AFTER_MINUTES = 90      // INTEGER: waiting time before a routine patient is promoted
CONSTANT MAX_QUEUE_SIZE = 100            // INTEGER: maximum patients waiting at one time
CONSTANT FEVER_HIGH = 39.5               // REAL: high fever threshold in degrees Celsius
CONSTANT FEVER_MILD = 38.0               // REAL: mild fever threshold in degrees Celsius
CONSTANT MIN_AGE = 0, MAX_AGE = 120      // INTEGER: valid age range in years
CONSTANT MIN_TEMP = 34.0, MAX_TEMP = 43.0  // REAL: valid body temperature range

VARIABLE patientCount, servedCount, promotedCount : INTEGER
VARIABLE emergencyQueue, urgentQueue, routineQueue : LIST of Patient
VARIABLE running : BOOLEAN
RECORD Patient: ticket (STRING), name (STRING), age (INTEGER), temp (REAL), painScore (INTEGER),
illnessDays (INTEGER), isPregnant (BOOLEAN), vomiting (BOOLEAN), waitMinutes (INTEGER)
2. Main Program
PROGRAM CHC_Triage_System
SET patientCount = 0, servedCount = 0, promotedCount = 0
SET emergencyQueue, urgentQueue, routineQueue = empty lists
SET running = TRUE
WHILE running = TRUE DO
CALL displayMenu()
INPUT choice
IF choice = 1 THEN
CALL registerPatient()
ELSE IF choice = 2 THEN
CALL callNextPatient()
ELSE IF choice = 3 THEN
CALL displayQueueStatus()
ELSE IF choice = 4 THEN
CALL generateDailyReport()
ELSE IF choice = 5 THEN
SET running = FALSE
ELSE
OUTPUT "Invalid choice. Please enter 1 to 5."
END IF
END WHILE
OUTPUT "System closed. Daily records saved."
END PROGRAM
3. Function registerPatient
FUNCTION registerPatient()
REPEAT
INPUT name, age, temp, painScore, illnessDays, isPregnant, vomiting
INPUT dangerBreathing, dangerConvulsion, dangerBleeding, dangerUnconscious
SET isValid = validateInput(name, age, temp, painScore, illnessDays)
IF isValid = FALSE THEN
OUTPUT "Invalid data entered. Please re-enter patient details."
END IF
UNTIL isValid = TRUE
SET patientCount = patientCount + 1
SET hasDangerSign = dangerBreathing OR dangerConvulsion OR dangerBleeding OR dangerUnconscious
SET priority = calculateTriage(hasDangerSign, age, temp, isPregnant, painScore, illnessDays, vomiting)
CALL assignQueue(patient, priority)
END FUNCTION
4. Function validateInput
FUNCTION validateInput(name, age, temp, painScore, illnessDays) RETURNS BOOLEAN
IF name is empty THEN RETURN FALSE
IF age < MIN_AGE OR age > MAX_AGE THEN RETURN FALSE
IF temp < MIN_TEMP OR temp > MAX_TEMP THEN RETURN FALSE
IF painScore < 0 OR painScore > 10 THEN RETURN FALSE
IF illnessDays < 0 THEN RETURN FALSE
RETURN TRUE
END FUNCTION
5. Function calculateTriage
FUNCTION calculateTriage(hasDangerSign, age, temp, isPregnant, painScore, illnessDays, vomiting) RETURNS STRING
IF hasDangerSign = TRUE THEN
RETURN "EMERGENCY"
END IF
SET score = scoreTemperature(temp) + scoreAge(age) + scorePregnancy(isPregnant)
SET score = score + scorePain(painScore) + scoreDuration(illnessDays) + scoreVomiting(vomiting)
IF score >= URGENT_THRESHOLD THEN
RETURN "URGENT"
ELSE
RETURN "ROUTINE"
END IF
END FUNCTION
6. Scoring Functions
FUNCTION scoreTemperature(temp) RETURNS INTEGER
IF temp >= FEVER_HIGH THEN RETURN 3
ELSE IF temp >= FEVER_MILD THEN RETURN 2
ELSE RETURN 0
END FUNCTION




 
Figure 8: Module decomposition (hierarchy) of CHC-Triage
<img width="468" height="351" alt="image" src="https://github.com/user-attachments/assets/0539752b-381a-4bf4-b441-c344c67bb54a" />






