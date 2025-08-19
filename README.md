#include <iostream>
#include <chrono>
#include <thread>
#include <cstdlib>
#include <ctime>
using std::cout;
using std::cin;
using std::string;


int moveset;
int randomNumber;

namespace player_data{
    string NAME;
    int HP = 500;
    int ATK = 100;
    int HEAVY_ATK = 200;
}

namespace enemy_data{
    string NAME = "Noob";
    int HP = 300;
    int ATK = 100;
    int HEAVY_ATK = 500;
}

void sleep(){
    std::this_thread::sleep_for(std::chrono::milliseconds(1000));
}

void generate_random_number(){
    srand(time(0));
    randomNumber = (rand() % 2) + 1;
}

int main(){

    cout << "---------------------------- WELCOME ----------------------------\n";
    while(player_data::NAME.empty()){
        cout << "Enter your name: ";
        std::getline(std::cin, player_data::NAME);

        if(player_data::NAME.empty()){
            cout << "please, Enter your name! Try again.\n";
            sleep();
        }
    }

    cout << "Loading...\n";
    sleep();

    cout << "---------------------------- PLAYER'S DATA ----------------------------\n"
         << "NAME: " << player_data::NAME << '\n'
         << "HP: " << player_data::HP << '\n'
         << "ATK: " << player_data::ATK << '\n';

    sleep();
    cout << "Your enemy will be...\n";
    sleep();

    cout << "---------------------------- ENEMY' DATA ----------------------------\n"
         << "NAME: " << enemy_data::NAME << '\n'
         << "HP: " << enemy_data::HP << '\n'
         << "ATK: " << enemy_data::ATK << '\n';

    sleep();
    cout << "Proceeding for gameplay...\n";
    sleep();

    do{

        cout << "---------------------------- GAMEPLAY ----------------------------\n"
            << "1. Light Attack\n"
            << "2. Heavy Attack\n"
            << "Please, choose your next move (1/2): ";
        cin >> moveset;

        cout << "Attacking...\n";
        sleep();

        if(moveset == 1){
            enemy_data::HP -= player_data::ATK;
            cout << "Enemy' health is now " << enemy_data::HP << '\n';
        }
        else if(moveset == 2){
            enemy_data::HP -= player_data::HEAVY_ATK;
            cout << "Enemy' health is now " << enemy_data::HP << '\n';
        }

        if(enemy_data::HP <=0){
            cout << "You win!\n";
            return 0;
        }
        else if(player_data::HP <= 0){
            cout << "You lose!\n";
            return 0;
        }

        sleep();
        cout << "The enemy is choosing his next moves..\n";
        sleep();

        generate_random_number();

        if(randomNumber == 1){
            player_data::HP -= enemy_data::ATK;
            cout << "Your health is now " << player_data::HP << '\n';
        }
        else if(randomNumber == 2){
            player_data::HP -= enemy_data::HEAVY_ATK;
            cout << "Your health is now " << player_data::HP << '\n';
        }

        sleep();
        cout << "Loading..\n";
        sleep();

        cout << "---------------------------- PLAYER'S DATA ----------------------------\n"
         << "NAME: " << player_data::NAME << '\n'
         << "HP: " << player_data::HP << '\n'
         << "ATK: " << player_data::ATK << '\n';

        if(enemy_data::HP <=0){
            cout << "You win!\n";
            return 0;
        }
        else if(player_data::HP <= 0){
            cout << "You lose!\n";
            return 0;
        }

    }while(enemy_data::HP > 0 || player_data::HP > 0);


    return 0;
}
