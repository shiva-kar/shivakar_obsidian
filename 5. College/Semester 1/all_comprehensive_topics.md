# Module I: Introduction to Computers

## 1. Introduction to Computers

Definition:

A computer is an electronic device that accepts raw data (input), processes it according to a set of instructions (program), stores the result, and produces output in a desired format.

- **Etymology:** Derived from the Latin word _computare_, meaning "to calculate."
    
- **Core Functionality:** It operates on the IPO cycle: **Input $\rightarrow$ Process $\rightarrow$ Output**.
    

## 2. History and Evolution

The evolution of computers is generally divided into the "Pre-Electronic" and "Electronic" eras.

### Pre-Electronic Era (Mechanical)

- **Abacus (ca. 2500 BC):** The first known calculating device. Used beads on rods for addition/subtraction.
    
- **Napier’s Bones (1614):** Invented by John Napier. A set of rods used for multiplication and division using logarithms.
    
- **Pascaline (1642):** Invented by Blaise Pascal. The first mechanical calculator using gears and wheels, capable of addition and subtraction.
    
- **Difference Engine (1822):** Designed by **Charles Babbage** (Father of the Computer) to calculate polynomial functions.
    
- **Analytical Engine (1833):** Babbage's successor to the Difference Engine. It is considered the first general-purpose computer design because it had the fundamental components: Input, Store (Memory), Mill (Processor), and Output.
    
- **Ada Lovelace:** She wrote the first algorithm for the Analytical Engine, making her the **first computer programmer**.
    
- **Hollerith’s Tabulating Machine (1890):** Invented by Herman Hollerith using punch cards. This company later became **IBM**.
    

## 3. Generations of Computer

Computers are classified into five generations based on the technology used for processing data.

|**Generation**|**Period**|**Core Technology**|**Memory/Storage**|**Language**|**Examples**|
|---|---|---|---|---|---|
|**First**|1940–1956|**Vacuum Tubes**|Magnetic Drums|Machine Code (0s & 1s)|ENIAC, UNIVAC, EDVAC|
|**Second**|1956–1963|**Transistors**|Magnetic Core|Assembly, Early High-Level (COBOL, FORTRAN)|IBM 7094, CDC 1604|
|**Third**|1964–1971|**Integrated Circuits (ICs)**|Large Magnetic Core|High-Level Languages|IBM 360, PDP-8|
|**Fourth**|1971–Present|**Microprocessors (VLSI)**|Semiconductor (RAM/ROM)|C, C++, Java, Python|Intel 4004, Apple II, PCs|
|**Fifth**|Present–Future|**AI & ULSI**|Optical/Bio-chips|Natural Language Processing|Robotics, Quantum Comp.|

- **VLSI:** Very Large Scale Integration.
    
- **ULSI:** Ultra Large Scale Integration.
    

## 4. Applications of Computers

Computers are ubiquitous today. Key domains include:

1. **Education:** E-learning, digital libraries, research (like what you are doing now).
    
2. **Business:** Payroll, inventory management, e-commerce, banking (ATMs, UPI).
    
3. **Healthcare:** MRI/CT scans, robotic surgery, patient record maintenance.
    
4. **Science & Engineering:** Weather forecasting, CAD (Computer-Aided Design), space exploration.
    
5. **Entertainment:** Gaming, VFX, music production, streaming.
    
6. **Government:** Aadhar databases, tax filing, census management.
    

## 5. Capabilities and Limitations

### Capabilities (Characteristics)

1. **Speed:** Can perform millions of instructions per second (MIPS).
    
2. **Accuracy:** Results are 100% accurate provided the input is correct.
    
3. **Diligence:** Unlike humans, computers do not get tired or lose concentration.
    
4. **Versatility:** Can perform completely different tasks (e.g., playing music vs. calculating spreadsheets) simultaneously.
    
5. **Storage Capacity:** Can store massive amounts of data in a small physical space.
    

### Limitations

1. **No IQ (Zero Intelligence):** It cannot think; it strictly follows instructions.
    
2. **GIGO (Garbage In, Garbage Out):** If you give wrong input, you get wrong output.
    
3. **Dependency:** Fully dependent on electricity and human instructions.
    
4. **No Heuristics:** Cannot learn from past mistakes (unless programmed with specific Machine Learning algorithms).
    

## 6. Components of a Computer System

A computer system consists of hardware organized into a specific architecture (Von Neumann Architecture).

### A. Central Processing Unit (CPU)

The "Brain" of the computer. It consists of:

**1. Control Unit (CU)**

- **Function:** It does not process data itself. instead, it acts as the "traffic police."
    
- **Role:** It fetches instructions from memory, decodes them, and directs the ALU and I/O devices on what to do. It controls the flow of data via buses.
    

**2. Arithmetic Logic Unit (ALU)**

- **Function:** Performs the actual execution.
    
- **Arithmetic Section:** Addition, subtraction, multiplication, division.
    
- **Logic Section:** Comparisons (Is A > B?), AND, OR, NOT operations.
    

### B. Input/Output (I/O) Devices

- **Input Devices:** Convert human signals into machine-readable digital form.
    
    - _Examples:_ Keyboard, Mouse, Scanner, Microphone, OCR, OMR.
        
- **Output Devices:** Convert machine digital data into human-readable form.
    
    - _Examples:_ Monitor (VDU), Printer (Laser/Inkjet), Speakers, Plotter.
        

## 7. Memory

Memory is the workspace for the computer. It is generally divided into Primary (Main) and Secondary memory. Your syllabus focuses on Primary types.

### A. RAM (Random Access Memory)

- **Type:** Volatile (Data is lost when power is turned off).
    
- **Usage:** Stores the operating system, application programs, and data currently in use.
    
- **Types of RAM:**
    
    1. **SRAM (Static RAM):** Fast, expensive, uses flip-flops to hold data. Used for **Cache Memory**.
        
    2. **DRAM (Dynamic RAM):** Slower, cheaper, uses capacitors that leak charge and need "refreshing" thousands of times per second. Used for standard system RAM (DDR3, DDR4).
        

### B. ROM (Read Only Memory)

- **Type:** Non-Volatile (Data remains even without power).
    
- **Usage:** Stores the **BIOS** (Basic Input Output System) and Bootstrap loader (instructions to start the computer).
    

**Types of ROM:**

1. **PROM (Programmable ROM):** Manufactured blank. The user can write data to it once. Once written, it cannot be changed.
    
2. **EPROM (Erasable Programmable ROM):** Can be erased by exposing it to **Ultraviolet (UV) light** through a quartz window on the chip, then rewritten.
    
3. **EEPROM (Electrically Erasable Programmable ROM):** Can be erased and rewritten electrically without removing the chip from the computer. Slower than RAM.
    

### C. Flash Memory

- **Definition:** A specific type of EEPROM.
    
- **Characteristics:** It is non-volatile, durable, and can be erased in blocks (rather than byte-by-byte like traditional EEPROM), making it faster.
    
- **Usage:** USB Pen drives, SSDs (Solid State Drives), SD Cards, and BIOS chips in modern computers.
    

### D. Other Types

- **Cache Memory:** Extremely fast, small memory located between the CPU and RAM. It holds frequently accessed data to speed up processing.
    
- **Registers:** The smallest, fastest memory units located _inside_ the CPU (e.g., Accumulator, Program Counter).
    

---

# Module II: Introduction to Number Systems

## 1. Introduction to Number Systems

In computing, a number system is defined by its **Base** (or Radix), which indicates the number of unique digits used to represent values.

### A. Decimal Number System (Base 10)

- **Digits:** 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
    
- **Usage:** The standard system used by humans.
    
- **Positional Value:** Powers of 10 ($10^0, 10^1, 10^2...$)
    

### B. Binary Number System (Base 2)

- **Digits:** 0, 1
    
- **Usage:** The native language of computers (0 = Off/Low Voltage, 1 = On/High Voltage).
    
- **Positional Value:** Powers of 2 ($2^0, 2^1, 2^2...$)
    
- _Example:_ $(101)_2 = 1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 = 5_{10}$
    

### C. Octal Number System (Base 8)

- **Digits:** 0, 1, 2, 3, 4, 5, 6, 7
    
- **Usage:** Used in early computing to shorten long binary strings (since 3 binary bits = 1 octal digit).
    
- **Positional Value:** Powers of 8.
    

### D. Hexadecimal Number System (Base 16)

- **Digits:** 0-9 and A-F (where A=10, B=11, C=12, D=13, E=14, F=15).
    
- **Usage:** Standard for memory addresses (e.g., `0x7FFF`), MAC addresses, and color codes.
    
- **Relationship:** 1 Hex digit = 4 Binary bits (Nibble).
    

### E. BCD (Binary Coded Decimal)

- **Definition:** A system where _each individual digit_ of a decimal number is represented by its own 4-bit binary sequence.
    
- **Difference from Pure Binary:**
    
    - **Decimal 12 in Binary:** $1100_2$
        
    - **Decimal 12 in BCD:** $0001$ (for 1) $0010$ (for 2) $\rightarrow 00010010_{BCD}$
        
- **Usage:** Digital clocks, calculators (where precise decimal display is needed without rounding errors).
    

---

## 2. Conversion Between Number Systems

![Image of Number System Conversion Table](https://encrypted-tbn2.gstatic.com/licensed-image?q=tbn:ANd9GcTzpZzTDsrDM9vK-qq_7C4ngHgF6rtX4sxbo4aO66w8OT_as0ByIw8hIQj3EKvavBVbkf0maSoB0s17TPkt_owLh9NMGusVQ_p9ULffvx3KLoSJ3cY)

### A. Decimal to Others (Division Method)

To convert Decimal to Binary/Octal/Hex, repeatedly **divide** the integer part by the base and record the **remainders** in reverse order (Bottom-Up).

**Example: Convert $25_{10}$ to Binary**

1. $25 \div 2 = 12$ (Remainder **1**)
    
2. $12 \div 2 = 6$ (Remainder **0**)
    
3. $6 \div 2 = 3$ (Remainder **0**)
    
4. $3 \div 2 = 1$ (Remainder **1**)
    
5. $1 \div 2 = 0$ (Remainder **1**)
    

- Result (Bottom-Up): **$11001_2$**
    

### B. Others to Decimal (Multiplication Method)

Multiply each digit by its positional weight (Base power).

**Example: Convert $1A_{16}$ to Decimal**

- $1 \times 16^1 + A(10) \times 16^0$
    
- $= 16 + 10$
    
- $= 26_{10}$
    

### C. Binary $\leftrightarrow$ Octal (Grouping of 3)

- **Binary to Octal:** Group bits in sets of **3** starting from the right (LSB).
    
    - $110101_2 \rightarrow (110)(101) \rightarrow 65_8$
        
- **Octal to Binary:** Convert each octal digit to 3 bits.
    
    - $72_8 \rightarrow (111)(010) \rightarrow 111010_2$
        

### D. Binary $\leftrightarrow$ Hexadecimal (Grouping of 4)

- **Binary to Hex:** Group bits in sets of **4** starting from the right.
    
    - $11101011_2 \rightarrow (1110)(1011) \rightarrow E B_{16}$
        
- **Hex to Binary:** Convert each hex digit to 4 bits.
    

---

## 3. Binary Complements

Complements are used in computers to represent negative numbers and perform subtraction using addition logic.

### A. One’s Complement

- **Method:** Simply invert every bit (change 0 to 1, and 1 to 0).
    
- **Example:**
    
    - Original (Binary for 5): `0101`
        
    - 1’s Complement: `1010`
        

### B. Two’s Complement

- **Method:** 1’s Complement + 1.
    
- **Usage:** This is how modern computers store negative integers. It eliminates the problem of having two zeros (+0 and -0).
    
- **Example:** Find -5 using 4-bit 2's complement.
    
    1. Write +5 in binary: `0101`
        
    2. Find 1’s Complement: `1010`
        
    3. Add 1: `1010 + 1 = 1011`
        
    
    - Result: `1011` represents -5.
        

---

## 4. Boolean Algebra and Laws

Boolean Algebra deals with binary variables and logic operations. It is the mathematical foundation of digital circuits.

**Basic Operators:**

1. **AND ($\cdot$):** Output is 1 only if _both_ inputs are 1.
    
2. **OR ($+$):** Output is 1 if _at least one_ input is 1.
    
3. **NOT ($'$ or $\bar{A}$):** Inverts the input (0 becomes 1).
    

### Fundamental Laws of Boolean Algebra

These laws are used to simplify logic circuits.

**1. Identity Law**

- $A + 0 = A$
    
- $A \cdot 1 = A$
    

**2. Null Law**

- $A + 1 = 1$
    
- $A \cdot 0 = 0$
    

**3. Idempotent Law**

- $A + A = A$
    
- $A \cdot A = A$
    

**4. Inverse Law**

- $A + \bar{A} = 1$
    
- $A \cdot \bar{A} = 0$
    

**5. Commutative Law**

- $A + B = B + A$
    
- $A \cdot B = B \cdot A$
    

**6. Associative Law**

- $(A + B) + C = A + (B + C)$
    
- $(A \cdot B) \cdot C = A \cdot (B \cdot C)$
    

**7. Distributive Law**

- $A \cdot (B + C) = (A \cdot B) + (A \cdot C)$
    
- $A + (B \cdot C) = (A + B) \cdot (A + C)$ _(Note: This second one is unique to Boolean algebra)_
    

8. De Morgan’s Theorems (Crucial)

Used to break bars (inversions) over variables.

- **Theorem 1:** $\overline{A \cdot B} = \bar{A} + \bar{B}$ (The complement of a product is the sum of the complements).
    
- **Theorem 2:** $\overline{A + B} = \bar{A} \cdot \bar{B}$ (The complement of a sum is the product of the complements).
    

---
# Module III: Introduction to IT

## 1. Introduction to IT (Information Technology)

Definition:

Information Technology (IT) is the study, design, development, implementation, support, or management of computer-based information systems, particularly software applications and computer hardware.

- **Core Concept:** It is the convergence of **Computer Technology** (Hardware/Software) and **Communication Technology** (Networking).
    

## 2. Need for IT

IT is essential in the modern world for:

1. **Speed and Efficiency:** Automating manual tasks to save time.
    
2. **Data Storage:** Managing massive volumes of data (Big Data) that physical files cannot handle.
    
3. **Communication:** Enabling instant global connectivity (Email, VoIP).
    
4. **Decision Making:** providing accurate, real-time data for business analysis.
    
5. **Cost Reduction:** Reducing paper waste and labor costs.
    

## 3. Information Storage and Processing

- **Data vs. Information:**
    
    - **Data:** Raw, unorganized facts (e.g., "25", "John", "Red").
        
    - **Information:** Processed data that has meaning (e.g., "John is 25 years old and likes Red").
        
- **Processing Cycle:**
    
    1. **Collection:** Gathering raw data.
        
    2. **Preparation:** Filtering/Validation.
        
    3. **Input:** Entering into the system.
        
    4. **Processing:** Calculation, classification, sorting.
        
    5. **Output:** Generating reports.
        
    6. **Storage:** Saving for future use.
        

## 4. Internet and WWW

### The Internet

- **Definition:** A global system of interconnected computer networks that use the standard Internet Protocol Suite (**TCP/IP**) to serve billions of users worldwide. It is the "hardware" or infrastructure (cables, routers, servers).
    
- **Key Services:** Email, File Transfer (FTP), Remote Login.
    

### The WWW (World Wide Web)

- **Definition:** An information space where documents and other web resources are identified by URLs, interlinked by hypertext links, and accessible via the Internet. It is a "service" running _on top_ of the Internet.
    
- **Invented by:** Tim Berners-Lee (1989).
    
- **Core Technologies:**
    
    1. **HTML:** Formatting language.
        
    2. **HTTP/HTTPS:** Protocol for transferring web pages.
        
    3. **URL:** Address of the page.
        

## 5. Different Types of Software

Software is a collection of instructions that enable the user to interact with a computer.

### A. System Software

Programs designed to run the computer's hardware and application programs.

1. **Operating System (OS):** Windows, Linux, macOS.
    
2. **Device Drivers:** Translators between hardware and OS (e.g., Printer driver).
    
3. **Language Translators:** Compilers, Interpreters, Assemblers.
    

### B. Application Software

Programs designed for end-users to perform specific tasks.

1. **General Purpose:** Word processors (MS Word), Web Browsers (Chrome).
    
2. **Specific Purpose:** Hotel management systems, Billing software.
    

### C. Utility Software

Maintenance software to keep the system healthy.

- _Examples:_ Antivirus, Disk Cleanup, File Compression (WinRAR).
    

## 6. Introduction to Information Systems (IS)

An Information System is an organized combination of people, hardware, software, communications networks, and data resources that collects, transforms, and disseminates information in an organization.

- **TPS (Transaction Processing Systems):** Records daily routine transactions (e.g., Sales entry).
    
- **MIS (Management Information Systems):** Provides middle managers with reports on current performance.
    
- **DSS (Decision Support Systems):** Helps senior management make non-routine decisions.
    

## 7. Business Data Processing

The manipulation of data to produce meaningful information in a business context.

- **Cycle:** Origination $\rightarrow$ Input $\rightarrow$ Processing $\rightarrow$ Output $\rightarrow$ Distribution $\rightarrow$ Storage.
    
- **Goal:** To convert trade/business data (orders, invoices) into financial reports and analytics.
    

---

# Module IV: Operating System

## 1. Definition and Use

Definition:

An Operating System (OS) is a system software that manages computer hardware, software resources, and provides common services for computer programs.

- **Analogy:** The OS is the "Government" of the computer; it doesn't do the work itself but provides the environment and rules for applications to work.
    
- **Core Functions:**
    
    1. **Process Management:** Creating/deleting processes.
        
    2. **Memory Management:** Allocating RAM.
        
    3. **File Management:** Organizing data on disks.
        
    4. **Device Management:** Controlling peripherals.
        
    5. **Security:** Password protection and user access.
        

## 2. Types of Operating Systems

### A. Batch Processing OS

- **Concept:** Similar jobs are grouped together into "batches" and submitted to the computer.
    
- **Mechanism:** The user does not interact with the computer directly. The operator feeds the deck of punch cards (batch).
    
- **Pros:** Efficient for high-volume, repetitive tasks (e.g., payroll).
    
- **Cons:** High turnaround time; difficult to debug.
    

### B. Multiprogramming OS

- **Concept:** Several programs are kept in the main memory (RAM) at the same time.
    
- **Mechanism:** When one program waits for I/O (e.g., waiting for user input), the CPU switches to another program to stay busy.
    
- **Goal:** Maximize CPU utilization.
    

### C. Multi-Tasking (Time-Sharing) OS

- **Concept:** A logical extension of multiprogramming. The CPU switches between tasks so rapidly that multiple users/programs feel they have the CPU all to themselves.
    
- **Mechanism:** Uses "Time Slicing" (Quantum). Each process gets a tiny slice of CPU time (e.g., 2 milliseconds).
    
- **Example:** Using Word while listening to Spotify and downloading a file.
    

### D. Multiprocessing OS

- **Concept:** Uses **two or more CPUs** (processors) within a single computer system.
    
- **Mechanism:** Parallel processing. Tasks are divided among different processors.
    
- **Pros:** greatly increases speed and reliability (if one CPU fails, others take over).
    

## 3. Data Communication

Definition: The exchange of data between two devices via some form of transmission medium (wire/wireless).

Components:

1. **Sender:** The device sending data.
    
2. **Receiver:** The device receiving data.
    
3. **Message:** The information (text, audio, video).
    
4. **Medium:** The physical path (Fiber optic, copper wire, air).
    
5. **Protocol:** The set of rules governing the exchange (e.g., TCP/IP).
    

---

# Module V: Introduction to Programming Concepts

## 1. Define Program & Process of Programming

- **Program:** A precise sequence of instructions written in a computer language to perform a specific task.
    
- **Programming:** The art and science of translating a problem solution into a language the computer can understand.
    
- **The Process (SDLC basics):**
    
    1. Problem Definition.
        
    2. Algorithm Design.
        
    3. Coding.
        
    4. Compilation/Testing (Debugging).
        
    5. Documentation & Maintenance.
        

## 2. Algorithms

Definition: A step-by-step logical procedure to solve a specific problem in a finite number of steps.

Characteristics:

- **Unambiguous:** Each step must be clear.
    
- **Finite:** Must end after a specific number of steps.
    
- **Input/Output:** Must accept input and yield output.
    

## 3. Flowcharts

**Definition:** A graphical representation of an algorithm.

### Basic Symbols

![Image of Flowchart Symbols](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcSzNAUP77gdfNnwx5rHrObamvucbRS4mYcKjfe0Z9EYK23F4gF8kSejg89woITOtI9x-3PwCKXGrUOTmmw_GNAwQDessQn9cAJfn4yr0piebTIh9MM)


1. **Oval (Terminal):** Start or Stop.
    
2. **Parallelogram:** Input or Output operations.
    
3. **Rectangle:** Processing (Calculations, variable assignment).
    
4. **Diamond:** Decision making (Yes/No questions).
    
5. **Arrows:** Flow lines indicating direction.
    
6. **Circle:** Connector (joining parts of a flowchart).
    

### Advantages and Limitations

- **Advantages:**
    
    - Better Communication: Pictures are easier to understand than text.
        
    - Effective Analysis: Helps identify logic errors early.
        
    - Documentation: Serves as a blueprint for the code.
        
- **Limitations:**
    
    - Complex for large programs.
        
    - Difficult to modify (requires redrawing).
        
    - Time-consuming to draw.
        

## 4. Pseudocodes

**Definition:** "False Code." A description of a computer programming algorithm that uses the structural conventions of a programming language but is intended for human reading rather than machine reading.

### Three Basic Logic Structures

Every computer program is built using these three logic structures:

**A. Sequence Logic**

- **Concept:** Instructions are executed one after another in a linear order.
    
- **Example:**
    
    Plaintext
    
    ```
    INPUT A
    INPUT B
    SUM = A + B
    PRINT SUM
    ```
    

**B. Selection Logic (Branching/Decision)**

- **Concept:** The program chooses a path based on a condition (True/False).
    
- **Example:**
    
    Plaintext
    
    ```
    IF Age > 18 THEN
       PRINT "Adult"
    ELSE
       PRINT "Minor"
    ENDIF
    ```
    

**C. Iteration Logic (Looping)**

- **Concept:** Repeating a set of instructions until a condition is met.
    
- **Example:**
    
    Plaintext
    
    ```
    WHILE Count < 10 DO
       PRINT Count
       Count = Count + 1
    ENDWHILE
    ```
    

### Advantages and Disadvantages of Pseudocode

- **Advantages:**
    
    - Language independent (can be translated to C, Java, Python easily).
        
    - Easier to write and modify than flowcharts.
        
    - Allows focus on logic without worrying about syntax errors.
        
- **Disadvantages:**
    
    - No visual representation of logic flow (unlike flowcharts).
        
    - No standard syntax (everyone writes it slightly differently).
        

---