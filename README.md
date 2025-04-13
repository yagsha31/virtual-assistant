import tkinter as tk

class QuizApp:
    def __init__(self, master):
        
        self.master = master
        master.title("Quiz Game")
        master.geometry("400x300")  # Set the size of the window

        self.score = 0
        self.question_index = 0
        self.points_per_correct_answer = 4

        self.questions = [
            {"question": "Q1. What is the primary task of the compilar ? ",
             "options": ['A) To convert source code into machine code ', 'B) To execute the program ', 
                         'C) To provide source code into machine code ', 'D) To debug the code '], 
             "answer": 'A) To convert source code into machine code '},
            
            {"question": "Q2. Which of the following is not Operating System ?", 
             "options": ['A) Linux ', 'B) MinGW-w64 ', 'C) Windows ', 'D) MacOS '], 
             "answer": 'B) MinGW-w64 '},
            
            {"question": "Q3. What is the full form of GUI ?", 
             "options": ['A) Graphical User Interface ', 'B) Graphical User Interchange ', 'C) Graphical User Interport ',
                         'D) Graphical Usage Interface '], 
             "answer": 'A) Graphical User Interface '},
            
            {"question": "Q4. Which keyword is used for function in Python language ? ", 
             "options": ['A) Function','B) def','C) fun','D)Define'],"answer":'B) def'},
            
            {"question": "Q5. Which of the following is a python tuple ?",
             "options": ['A) [1,2,3]','B) (1,2,3)','C) {1,2,3}','D) {}'],
             "answer": 'B) (1,2,3)'},
            
              
            {"question": "Q6. Which of the follwing is a immutable in python ?",
             "options": ['A) lists','B) sets','C) dictionaries','D) tuples'],
             "answer": 'D) tuples'},     
            {"question": "Q7. In programming, what does the term 'data type' refer to ?",
             "options": ['A) A location in memory','B) The size of Ram','C) The kind of data that can be stored',
                         'D) A programming language syntex '],
             "answer": 'C) The kind of data that can be stored'},
               
            {"question": "Q8. Which of the follwing is considered a low-lavel programming language ?",
             "options": ['A) C++','B) Python','C) Assembly','D) java'],
             "answer": 'C) Assembly'},
               
            {"question": "Q9. In programming, What is named storage location in memory called ?",
             "options": ['A) Constant','B) Array','C) Function','D) Variable'],
             "answer": 'D) Variable'},     
            {"question": "Q10. What is the main role of a Memory Manager in a computer system ?",
             "options": ['A) To manage process in the CPU','B) To manage secondary storage devices',
                         'C) To manage the flow of data in networks','D) To manage and allocate RAM for process'],
             "answer": 'A) To manage process in the CPU'}      
        ]
        
        self.max_score = len(self.questions) * self.points_per_correct_answer  # Calculate maximum score

        self.question_label = tk.Label(master, text=self.questions[self.question_index]['question'], wraplength=350)
        self.question_label.pack(pady=20)

        self.var = tk.StringVar()
        self.options = []
        for option in self.questions[self.question_index]['options']:
            b = tk.Radiobutton(master, text=option, variable=self.var, value=option, command=self.check_answer)
            b.pack(anchor='w')
            self.options.append(b)

        self.next_button = tk.Button(master, text="Next", command=self.next_question)
        self.next_button.pack(pady=20)

        self.result_text = tk.Label(master, text="")
        self.result_text.pack()

    def check_answer(self):
        if self.var.get() == self.questions[self.question_index]['answer']:
            self.score += self.points_per_correct_answer  # Add points for correct answer
            self.result_text.config(text=f"Correct! +{self.points_per_correct_answer} points")
        else:
            self.result_text.config(text="Wrong!")

    def next_question(self):
        if self.question_index < len(self.questions) - 1:
            self.question_index += 1
            self.question_label.config(text=self.questions[self.question_index]['question'])
            for b, option in zip(self.options, self.questions[self.question_index]['options']):
                b.config(text=option, value=option)
            self.var.set(None)  # Clear selection
            self.result_text.config(text="")
        else:
            self.display_score()

    def display_score(self):
        for b in self.options:
            b.pack_forget()
        self.next_button.pack_forget()
        self.result_text.config(text=f"Game Over. Your final score: {self.score} out of {self.max_score}")

root = tk.Tk()
app = QuizApp(root)
root.mainloop()



