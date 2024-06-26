#include <iostream>
#include <cstdlib>
#include <time.h>
using namespace std;

int gameExit = 0;
class Tic_Tac_Toe
{
private:
    char position[9] = {'1', '2', '3', '4', '5', '6', '7', '8', '9'};

public:
    void checkResult(void);
    void printBody();
    void playGame(int);
    void placeSign(int, char);
};

void Tic_Tac_Toe::checkResult()
{
    if ((position[0] == 'X' && position[1] == 'X' && position[2] == 'X') ||
        (position[3] == 'X' && position[4] == 'X' && position[5] == 'X') ||
        (position[6] == 'X' && position[7] == 'X' && position[8] == 'X') ||
        (position[0] == 'X' && position[3] == 'X' && position[6] == 'X') ||
        (position[1] == 'X' && position[4] == 'X' && position[7] == 'X') ||
        (position[2] == 'X' && position[5] == 'X' && position[8] == 'X') ||
        (position[0] == 'X' && position[4] == 'X' && position[8] == 'X') ||
        (position[2] == 'X' && position[4] == 'X' && position[6] == 'X'))
    {
        cout << "\nCongrats! X won the game\n\n";
        exit(0);
    }
    else if ((position[0] == 'O' && position[1] == 'O' && position[2] == 'O') ||
             (position[3] == 'O' && position[4] == 'O' && position[5] == 'O') ||
             (position[6] == 'O' && position[7] == 'O' && position[8] == 'O') ||
             (position[0] == 'O' && position[3] == 'O' && position[6] == 'O') ||
             (position[1] == 'O' && position[4] == 'O' && position[7] == 'O') ||
             (position[2] == 'O' && position[5] == 'O' && position[8] == 'O') ||
             (position[0] == 'O' && position[4] == 'O' && position[8] == 'O') ||
             (position[2] == 'O' && position[4] == 'O' && position[6] == 'O'))
    {
        cout << "\nCongrats! O won the game\n\n";
        exit(0);
    }
    else if (gameExit == 9)
    {
        cout << "\nGame is draw!\n\n";
        exit(0);
    }
}

void Tic_Tac_Toe::printBody()
{
    cout << "\n*" << endl;
    cout << "|  " << position[0] << "  |  " << position[1] << "  |  " << position[2] << "  |" << endl;
    cout << "|*|" << endl;
    cout << "|  " << position[3] << "  |  " << position[4] << "  |  " << position[5] << "  |" << endl;
    cout << "|*|" << endl;
    cout << "|  " << position[6] << "  |  " << position[7] << "  |  " << position[8] << "  |" << endl;
    cout << "*" << endl;
}

void Tic_Tac_Toe::placeSign(int pos, char sign)
{
    pos = pos - 1;
    if (position[pos] != 'X' && position[pos] != 'O')
    {
        position[pos] = sign;
    }
    else
    {
        cout << "\nInvalid position try again!\n";
        if (sign == 'X' || sign == 'O')
        {
            cin.sync();
            cout << "\nChoose position to place your sign: ";
            cin >> pos;
            placeSign(pos, sign);
        }
    }
}

void Tic_Tac_Toe::playGame(int mode)
{
    int pos;
    srand(time(0));
    char currentSign = 'X';
    cout << "\nX is your sign and O is computer sign\n";
    printBody();

    while (1)
    {
        gameExit++;
        if (mode == 1)
        {
            cout << "\nChoose position to place your sign (" << currentSign << "): ";
            cin >> pos;
            placeSign(pos, currentSign);
            printBody();
            checkResult();
            currentSign = (currentSign == 'X') ? 'O' : 'X';
        }
        else if (mode == 2)
        {
            if (currentSign == 'X')
            {
                cout << "\nChoose position to place your sign: ";
                cin >> pos;
                placeSign(pos, 'X');
                printBody();
                checkResult();
            }
            else
            {
                pos = rand() % 9 + 1;
                cout << "\nComputer chose " << pos << " position to place sign\n";
                placeSign(pos, 'O');
                printBody();
                checkResult();
            }
            currentSign = (currentSign == 'X') ? 'O' : 'X';
        }
        else if (mode == 3)
        {
            cout << "\nChoose position to place your sign (" << currentSign << "): ";
            cin >> pos;
            placeSign(pos, currentSign);
            printBody();
            checkResult();
            currentSign = (currentSign == 'X') ? 'O' : 'X';
        }
    }
}

int main()
{
    int choose;
    Tic_Tac_Toe t1;
    cout << "\n   -:  WELCOME TO TIC TAC TOE GAME  :-\n\n";
    cout << "Choose game mode:" << endl;
    cout << "Press 1 for Player vs Player\n";
    cout << "Press 2 for Player vs Computer\n";
    cout << "Press 3 for Computer vs Computer\n";
again:
    cin.sync();
    cin >> choose;
    if (choose == 1 || choose == 2 || choose == 3)
    {
        t1.playGame(choose);
    }
    else
    {
        cout << "\nInvalid key pressed try again\n";
        goto again;
    }
    return 0;
}
