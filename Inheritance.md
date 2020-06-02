#include "wincursor.h"
#include <string>
using std::string;

enum Directions { LEFT, RIGHT, UP, DOWN };

class MyString : public String {
public:
	MyString(string s, size_t row = 0, size_t col = 0) :
		String(s, row, col) {}
	void Move(Directions d) {
		hide();
		switch (d) {
		case LEFT:
			setX(getX() - 1);
			break;
		case RIGHT:
			setX(getX() + 1);
			break;
		case DOWN:
			setY(getY() + 1);
			break;
		case UP:
			setY(getY() - 1);
			break;
		}
		show();
	}
};

int main() {
	Screen myScreen;
	MyString a("Q", 10, 10);
	a.show();
	int c = myScreen.key();
	while (c != 'q') {
		switch (c) {
		case 'h':
			a.Move(LEFT);
			break;
		case 'l':
			a.Move(RIGHT);
			break;
		case 'j':
			a.Move(DOWN);
			break;
		case 'k':
			a.Move(UP);
			break;
		}
		c = myScreen.key();
	}

	return 0;
}
