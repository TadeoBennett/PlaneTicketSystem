#include <iostream>
using namespace std;

void menu(string company){
	cout<<"   "<<company<<"    "<<endl;
	cout<<"__________________"<<endl;
	cout<<"|1. Reserve      |"<<endl;
	cout<<"|2. Print Ticket |"<<endl;
	cout<<"|3. View Seats   |"<<endl;
	cout<<"|4. Exit         |"<<endl;
	cout<<"|________________|"<<endl;
	cout<<"CHOICE: ";
}

void Reserve_seat(){	
	cout<< "________________________" << endl ;
	cout<< "| Select the seat type | " << endl ;
	cout<< "|______________________|" << endl ;
	cout<< "| 1 First Class        |" << endl ;
	cout<< "| 2 Economy Class      |" << endl ;
	cout<< "|______________________|" << endl ;
	cout<< "Class Type: ";
}

void ticket(string name, char seattype, string company, int seatnumber){
	string seat;
	if(seattype == 'F'){seat = "First Class";}
	else if (seattype == 'E'){seat = "Economy Class";}
	if(name == ""){
		name = "Unreserved Seat";
	}
	
	cout<<"________________________________"<<endl;
	cout<<"|         "<<company<<"         "<<endl;	
	cout<<"|                               "<<endl;	
	cout<<"| Name:  "<<name<<"             "<<endl;	
	cout<<"|                               "<<endl;	
	cout<<"| Reservation: "<<seat<<"       "<<endl;	
	cout<<"|                               "<<endl;	
	cout<<"| Ticket Number: "<<seatnumber<<endl;
	cout<<"|_______________________________"<<endl;	
}

void viewseats(string * persons){			
	for(int i= 0; i<10; i++){
		if(i==0){cout<<"*** First Class Seats ***"<<endl;}
		if(i==4){cout<<"*** Economy Class Seats ***"<<endl;}
		cout<<"Seat "<<i+1<<": "<<persons[i]<<endl;
	}	
}


void table(int *P) {
	cout << "                                         ___          " << endl ;
	cout << "                                        /   /                  " << endl ;
	cout << "                                       /    /              " << endl ;
	cout << "                                      /     /                " << endl ;
	cout << "                                     /      /        " << endl ;
	cout << "                                    /       /        " << endl ;
	cout << "                                   /        /                         ____" << endl ;
	cout << "                                  /        /                         /   /" << endl ;
	cout << "                                 /        /                         /    /" << endl ;
	cout << "                                /         |                        /     /" << endl ;
	cout << "                               /          |                       /      / " << endl ;
	cout << "              ________________/___________|_____________________ /       /" << endl ;
	cout << "  ___________/  FIRST CLASS               ECONOMY CLASS        \\/________/" << endl ;
	cout << " /              ["<<P[0] <<"]       ["<<P[2] <<"]      ["<<P[4] <<"]   ["<<P[6] <<"]    ["<<P[8] <<"]                       \\ " << endl ;
	cout << "(|                                                                         )--" << endl ;
	cout << " \\___________   ["<<P[1]<<"]       ["<<P[3]<<"]      ["<<P[5]<<"]   ["<<P[7]<<"]   ["<<P[ 9 ]<<"]             __________/" << endl ;
	cout << "             \\________________________________________________/\\         \\ " << endl ;
	cout << "                              \\           |                      \\        \\  "    << endl ;
	cout << "                               \\          |                       \\       \\ " << endl ;
	cout << "                                \\         |                        \\      \\ " << endl ;
	cout << "                                 \\        \\                         \\     \\ " << endl ;
	cout << "                                  \\        \\                         \\____\\ " << endl ;
	cout << "                                   \\        \\                    " << endl ;
	cout << "                                    \\       \\                                       " << endl ;
	cout << "                                     \\      \\                           " << endl ;
	cout << "                                      \\     \\                      " << endl ;
	cout << "                                       \\    \\              " << endl ;
	cout << "                                        \\___\\              " << endl ;
}


int main(){
	int choice, classtype, movepassenger, reservations, option; 
	string company, name;
	string Persons[10];
	int firstclass_space = 4, economyclass_space = 6;
	int numbers[10] = {1, 2, 3, 4, 5 ,6, 7 , 8, 9, 10};
	char SeatTypes[10] = {'F', 'F', 'F', 'F', 'E', 'E', 'E', 'E', 'E', 'E'};
	int fposition = 0, eposition = 4;//used to track the index of arrays of reservations that can be made
	
	cout << "\t/* Hello, Welcome to the new Airline Reservation System *\\\n " << endl ;
	cout << "What is the Companies Name ? " << endl ;
	getline(cin, company); // gets the full name of company 
	system("CLS"); // clears screen
	cout << "\n\tYour Company " << company << " was registered \n" << endl ;
	system ("pause");
	system ("CLS");
	
	cout << "Here is the menu ! \n " << endl ;
	menu(company);
	cin>>choice;
	int i;
		
do{
	switch(choice)
	{
		case 1://Reservation
			table(numbers);
			Reserve_seat();
			cin>>classtype; cin.ignore();
			system("CLS") ;
//------------------------------------------------------------------------------------------------
			if (classtype == 1){//First Class
				cout<<"There are "<<firstclass_space<<" seats available."<<endl;
				cout<<"Number of Reservations: "; cin>>reservations; cin.ignore();
				if(reservations>firstclass_space){//if first class reservations are full
					cout<<"Not Enough Space for this class"<<endl;
					cout<<"Would you like to make a reservation in the Economy Class? (1)Yes, (2)No:"<<endl;
					cout<<"CHOICE: "; cin>>movepassenger;
					if(movepassenger == 1){
						cout<<"There are "<<economyclass_space<<" seats available."<<endl;
						cout<<"Number of Reservations: "; cin>>reservations; cin.ignore();
						if(reservations>economyclass_space){
							cout<<"Economy Class and First Class Reservations are Full"<<endl;
							cout<<"-->>Exiting<<--"<<endl;
						}
						else if (reservations <= economyclass_space){//reservations are not full
							for(i = 4; i <= reservations+5; i++){//loop until it finds an empty space and corresponding reservation
								if(SeatTypes[i+5] == 'E' && Persons[i+5] == ""){
									cout<<"Enter your first and last name: "; getline(cin, name);
									Persons[i+5] = name;
									economyclass_space -= 1;
								}
							}//end loop that gets names for the economy class reservations
							cout<<"Reservations Made"<<endl;
						}//end if reservations were not full for economy class
					}//end if statement where movepassenger == 1.
					else{cout<<"-->>Exiting<<--"<<endl;}//if move passenger = 2 then it exits		
				}
				else if(reservations<=firstclass_space){//if first class reservations are not full
					for(i = 0; i < reservations; i++){//loop until it finds an empty space and corresponding reservation
						if(SeatTypes[fposition] == 'F' && Persons[fposition] == ""){
							cout<<"Enter your first and last name: "; getline(cin, name);
							Persons[fposition] = name;
							firstclass_space -= 1;
							fposition += 1;
						}				
					}//end loop that gets names for the first class reservations
					int spaces = reservations;
					cout<<"Reservations Made"<<endl;
				}//end if reservations were not full for first class
			}//end if classtype was 1
//-------------------------------------------------------------------------------------------------------------------------------------------------			
			else if(classtype == 2){//Economy Class
			cout<<"There are "<<economyclass_space<<" seats available."<<endl;
				cout<<"Number of Reservations: "; cin>>reservations;cin.ignore();
				if(reservations>economyclass_space){//if economy class reservations are full
					cout<<"Not Enough Space for this class"<<endl;
					cout<<"Would you like to make a reservation in the First Class? (1)Yes, (2)No:"<<endl;
					cout<<"CHOICE: "; cin>>movepassenger;
					if(movepassenger == 1){
						cout<<"There are "<<firstclass_space<<" seats available."<<endl;
						cout<<"Number of Reservations: "; cin>>reservations;cin.ignore();
						if(reservations>firstclass_space){
							cout<<"First Class and Economy Reservations are Full"<<endl;
							cout<<"-->>Exiting<<--"<<endl;
						}
						else if (reservations <= firstclass_space){//reservations are not full
							for(i = 0; i < reservations; i++){//loop until it finds an empty space and corresponding reservation
								if(SeatTypes[fposition] == 'F' && Persons[fposition] == ""){
									cout<<"Enter your first and last name: "; getline(cin, name);
									Persons[fposition] = name;
									firstclass_space -= 1;
									fposition += 1;
								}
							}//end loop that gets names for the first class reservations
							cout<<"Reservations Made"<<endl;
						}//end if reservations were not full for first class
					}//end if statement where movepassenger == 1.
					else{cout<<"-->>Exiting<<--"<<endl;}//if move passenger = 2 then it exits		
				}
				else if(reservations<=economyclass_space){//if economy class reservations are not full
					for(i = 0; i < reservations; i++){//loop until it finds an empty space and corresponding reservation
						if(SeatTypes[eposition] == 'E' && Persons[eposition] == ""){
							cout<<"Enter your first and last name: "; getline(cin, name);
							Persons[eposition] = name;
							economyclass_space -= 1;
							eposition += 1;
						}					
					}//end loop that gets names for the economy class reservations
					cout<<"Reservations Made"<<endl;
				}//end if reservations were not full for economy class
			}//end if classtype was 2	
//-------------------------------------------------------------------------------------------------------------------------------------------------					
			else{
				cout<<"-->>Invalid<<--"<<endl;
			}
		break;
	
		case 2://Print Ticket
			cout<<"Print an Individual's ticket(1) or all tickets(2)?: ";
			cin>>option;
			switch(option){
				case 1:
					cout<<"Which seat number would you to print(1-10)?: ";
					cin>>option;					
					while(option>10)//loop while its invalid(greater than 10) 
					{
						cout<<"Which seat number would you to print(1-10)?: ";
						cin>>option;	
					}
					cout<<endl;
					ticket(Persons[option-1], SeatTypes[option-1], company, numbers[option-1]);					
											
				break;
				
				case 2:
					for(i = 0; i<10; i++){					
						ticket(Persons[i], SeatTypes[i], company, numbers[i]);
						cout<<"any"<<endl;
					}
				
				break;
							
				default:
					cout<<"-->>Invalid Option<<--"<<endl;				
			}//end of switch			
		break;
		
		case 3://View Seats
			viewseats(Persons);
		break;
		
		case 4:
			choice = 4;
		break;
		
		default:
			cout<<"-->>Invalid Option<<--"<<endl;
			menu(company);
			cin>>choice;
	}//end of switch
	menu(company);
	cin>>choice;
}while(choice != 4);//end of while

cout<<"Program made by Tadeo Bennett"<<endl;
	
return 0;
}
