# jogo-1import random




class GameAgent:
    def __init__(self, max_attempts=3):
        self.secret_number = random.randint(1, 100)  # Número secreto aleatório entre 1 e 100
        self.max_attempts = max_attempts
        self.attempts = 0
        self.state = "Esperando tentativa"
        self.history = []  # Histórico de tentativas
        self.penalty_threshold = random.randint(1, 3)  # Limite aleatório de erros antes de penalidade

    def make_guess(self, guess):
        if self.attempts >= self.max_attempts:
            return f"Game Over! O número era {self.secret_number}."
        
        self.attempts += 1
        self.history.append(guess)

        if guess == self.secret_number:
            self.state = "Acertou!"
            return "Parabéns! Você acertou o número."
        
        # Penalidade mais severa: pode perder até duas tentativas extras
        if self.attempts % self.penalty_threshold == 0:
            penalty = random.randint(1, 2)
            self.attempts += penalty
        
        if self.attempts >= self.max_attempts:
            self.state = "Fim do jogo"
            return f"Game Over! O número era {self.secret_number}."
        
        # Dicas ainda mais vagas
        if abs(guess - self.secret_number) <= 5:
            self.state = "Tentativa errada (muito quente)"
            return "Muito quente! Mas ainda não acertou."
        elif abs(guess - self.secret_number) <= 15:
            self.state = "Tentativa errada (morno)"
            return "Morno... Talvez esteja perto."
        else:
            self.state = "Tentativa errada (muito frio)"
            return "Muito frio! Péssima tentativa!"
