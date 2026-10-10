[winky_bot.py](https://github.com/user-attachments/files/33275817/winky_bot.py)
"""
Winky Bot - A cute animated bot with multiple expressions
Make Winky come to life with beautiful ASCII art!
"""

import time
import os
from enum import Enum


class Expression(Enum):
    """Bot expression types"""
    HAPPY = "happy"
    WINK = "wink"
    SAD = "sad"
    ANGRY = "angry"
    CONFUSED = "confused"
    SLEEPY = "sleepy"
    LOVE = "love"
    EXCITED = "excited"


class WinkyBot:
    """A cute animated bot named Winky with multiple expressions"""

    def __init__(self, name: str = "Winky"):
        self.name = name
        self.current_expression = Expression.HAPPY

    def clear_screen(self):
        """Clear terminal screen"""
        os.system("clear" if os.name == "posix" else "cls")

    def print_header(self):
        """Print welcome header"""
        print("\n" + "=" * 50)
        print(f"  ✨ Welcome to {self.name} Bot! ✨".center(50))
        print("=" * 50 + "\n")

    def get_face(self, expression: Expression) -> str:
        """Get ASCII art face for given expression"""

        faces = {
            Expression.HAPPY: """
        ╔════════════╗
        ║  (◕ ◡ ◕)  ║
        ║     ♥      ║
        ╚════════════╝
        """,
            Expression.WINK: """
        ╔════════════╗
        ║  (◕ ◡ ◉)  ║
        ║  ~wink~   ║
        ╚════════════╝
        """,
            Expression.SAD: """
        ╔════════════╗
        ║  (◕ ︿ ◕)  ║
        ║  I'm sad  ║
        ╚════════════╝
        """,
            Expression.ANGRY: """
        ╔════════════╗
        ║  (ಠ_ಠ)    ║
        ║ GRRRR!    ║
        ╚════════════╝
        """,
            Expression.CONFUSED: """
        ╔════════════╗
        ║  (◔_◔?)   ║
        ║ Confused? ║
        ╚════════════╝
        """,
            Expression.SLEEPY: """
        ╔════════════╗
        ║  (◕ - ◕)  ║
        ║  zzz...   ║
        ╚════════════╝
        """,
            Expression.LOVE: """
        ╔════════════╗
        ║  (◕ ♡ ◕)  ║
        ║ In love!  ║
        ╚════════════╝
        """,
            Expression.EXCITED: """
        ╔════════════╗
        ║  (◕ ▽ ◕)  ║
        ║  Yay!!!   ║
        ╚════════════╝
        """,
        }

        return faces.get(expression, faces[Expression.HAPPY])

    def display_expression(self, expression: Expression, duration: int = 3):
        """Display an expression for a duration"""
        self.current_expression = expression
        self.clear_screen()
        self.print_header()
        print(f"\n{self.name} is feeling: {expression.value.upper()}\n")
        print(self.get_face(expression))
        time.sleep(duration)

    def animate_sequence(self):
        """Play an animated sequence of expressions"""
        self.clear_screen()
        self.print_header()
        print("🎬 Watch Winky's emotional journey!\n")
        time.sleep(1)

        sequence = [
            (Expression.HAPPY, 2),
            (Expression.EXCITED, 2),
            (Expression.WINK, 2),
            (Expression.CONFUSED, 2),
            (Expression.LOVE, 2),
            (Expression.SLEEPY, 3),
        ]

        for expr, duration in sequence:
            self.clear_screen()
            self.print_header()
            print(f"\n{self.name} is feeling: {expr.value.upper()}\n")
            print(self.get_face(expr))
            time.sleep(duration)

        self.clear_screen()
        self.print_header()
        print(f"\n{self.name} is back to normal!\n")
        print(self.get_face(Expression.HAPPY))
        time.sleep(2)

    def show_menu(self):
        """Show interactive menu"""
        while True:
            self.clear_screen()
            self.print_header()
            print("Choose an expression to see Winky's face:\n")

            expressions = list(Expression)
            for idx, expr in enumerate(expressions, 1):
                print(f"{idx}. {expr.value.title()}")

            print(f"{len(expressions) + 1}. Watch Animation Sequence")
            print(f"{len(expressions) + 2}. Exit")

            try:
                choice = input("\n👉 Enter your choice (1-9): ").strip()

                if choice == str(len(expressions) + 2):
                    self.clear_screen()
                    print("\n" + "=" * 50)
                    print("  👋 Goodbye! Thanks for playing with Winky!".center(50))
                    print("=" * 50 + "\n")
                    break

                if choice == str(len(expressions) + 1):
                    self.animate_sequence()
                    input("\nPress Enter to continue...")
                    continue

                choice_idx = int(choice) - 1
                if 0 <= choice_idx < len(expressions):
                    self.display_expression(expressions[choice_idx], duration=4)
                    input("\nPress Enter to continue...")
                else:
                    print("Invalid choice! Please try again.")
                    time.sleep(2)

            except ValueError:
                print("Please enter a valid number!")
                time.sleep(2)
            except KeyboardInterrupt:
                self.clear_screen()
                print("\n" + "=" * 50)
                print("  👋 Goodbye! Thanks for playing with Winky!".center(50))
                print("=" * 50 + "\n")
                break

    def quick_show(self, expression_name: str):
        """Quickly show a specific expression"""
        try:
            expr = Expression[expression_name.upper()]
            self.clear_screen()
            self.print_header()
            print(f"\n{self.name} is feeling: {expr.value.upper()}\n")
            print(self.get_face(expr))
        except KeyError:
            print(f"Unknown expression: {expression_name}")
            print(f"Available: {', '.join([e.value for e in Expression])}")


def main():
    """Main entry point"""
    bot = WinkyBot("Winky")

    try:
        bot.show_menu()
    except Exception as e:
        print(f"Error: {e}")


if __name__ == "__main__":
    main()
