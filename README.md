import tkinter as tk
import random

class RockPaperScissors:
    def __init__(self):
        self.user_wins = 0
        self.computer_wins = 0
        self.ties = 0
        
        self.window = tk.Tk()
        self.window.title("Rock Paper Scissors")
        self.window.geometry("300x400")
        
        # Score display
        self.score_label = tk.Label(self.window, text="Score: You 0 - 0 Computer", 
                                   font=('Arial', 12))
        self.score_label.pack(pady=10)
        
        # Game buttons
        tk.Button(self.window, text="🪨 Rock", width=15, height=2, 
                 font=('Arial', 12), command=lambda: self.play('Rock')).pack(pady=5)
        tk.Button(self.window, text="📄 Paper", width=15, height=2, 
                 font=('Arial', 12), command=lambda: self.play('Paper')).pack(pady=5)
        tk.Button(self.window, text="✂️ Scissors", width=15, height=2, 
                 font=('Arial', 12), command=lambda: self.play('Scissors')).pack(pady=5)
        
        # Result display
        self.result_label = tk.Label(self.window, text="Make your choice!", 
                                    font=('Arial', 14), pady=20)
        self.result_label.pack()
        
        # Reset button
        tk.Button(self.window, text="Reset Score", 
                 command=self.reset_score).pack(pady=10)
    
    def decide_winner(self, user_choice, computer_choice):
        if user_choice == computer_choice:
            return "It's a Tie!"
        elif (user_choice == 'Rock' and computer_choice == 'Scissors') or \
             (user_choice == 'Scissors' and computer_choice == 'Paper') or \
             (user_choice == 'Paper' and computer_choice == 'Rock'):
            return "You Win!"
        else:
            return "Computer Wins!"
    
    def play(self, user_choice):
        computer_choice = random.choice(['Rock', 'Paper', 'Scissors'])
        result = self.decide_winner(user_choice, computer_choice)
        
        # Update score
        if "You Win" in result:
            self.user_wins += 1
        elif "Computer Wins" in result:
            self.computer_wins += 1
        else:
            self.ties += 1
        
        # Update displays
        self.result_label.config(text=f"Your choice: {user_choice}\n"
                                     f"Computer's choice: {computer_choice}\n{result}")
        self.score_label.config(text=f"Score: You {self.user_wins} - {self.computer_wins} Computer")
    
    def reset_score(self):
        self.user_wins = self.computer_wins = self.ties = 0
        self.score_label.config(text="Score: You 0 - 0 Computer")
        self.result_label.config(text="Make your choice!")
    
    def run(self):
        self.window.mainloop()

if __name__ == "__main__":
    game = RockPaperScissors()
    game.run()
 

 
