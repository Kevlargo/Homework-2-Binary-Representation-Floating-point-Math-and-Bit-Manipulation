// Adriel Largo
// Homework 2
// March 27th 2026
// CS 3339


#include <iostream>
#include <bitset> // per the assignment, lets me access bits
#include <cstring> // lets me use memcpy to copy bits
#include <cstdint> // need it for a 32 bit unsigned value
using namespace std;

// I will use a Class for the Bitset class for Floating Point Values

class BitsetFloat{
    public: // allow the following public access

    explicit BitsetFloat(float num){
        uint32_t val; // declare my variable as 32 bit unsigned and hold the value
        memcpy( &val, &num, sizeof(val)); // help with copying bits into Val
        newBits= bitset<32>(val); // puts the bits into newBits and i can acesses it 

    }

    // Function to help return the stored exponents as an integers
    //

    int Exponents() const{

    // declare variable and set to zero
    int exp = 0;
    // loop to get the 8 bits
    for ( int i =0;i<8;i++){
            if (newBits[23 + i]) // since exp is from bit 23 to bit 30
            exp|= (1<< i); // add to exp and shifts left by i


    } return exp;

    }

    // Function to print the bits in IEEE format

    void PrintBits() const{
    // print the sign 1 or 0 
        cout<< newBits[31]<< " ";
    // Print the exponent to the user using a for loop
        for (int i = 30 ; i>= 23; i--){
            cout<< newBits[i];
        }
        cout<< " ";

    //Print the Mantissa to user using for loop
    for ( int i =22;i>=0;i--){
        cout<< newBits[i];
    }
    }

    private:

        bitset<32> newBits;



};


// computing the threshold using a Function

float CalcThreshold( float increment ){

    uint32_t val; // declare my variable as 32 bit unsigned and hold the value
    memcpy( &val, &increment, sizeof(val)); // help with copying bits into Val

    uint32_t exp= (val >> 23) & 0xFF; // shift bits 23 to the right and holds 8 bottom bits
    uint32_t threshold_val = (exp +24)<< 23; // adds 24 to the exponent and shifts bits

    // declare variable
    float threshold ;
    // bits back to float using the memcpy function and return the value
    memcpy(&threshold, & threshold_val, sizeof(threshold));

    return threshold;
}




int main(int arg, char* arg2[])
{


    // if statement to check for exactly two arguments then print to user
    if (arg != 3){
            // per the assignment example i need exactly 2 arguments and the same output
        cout<<"usage:"<<endl;
        cout<<"        ./fp_overflow_checker loop_bound loop_counter"<<endl;
        cout<< endl;
        cout<<"        loop_bound is a positive floating-point value" << endl;
        cout<<"        loop_counter is a positive floating-point value" << endl;

        return 1;
    }

     // inputs using stof helps converts string to a float
    float loopBound =stof(arg2[1]);
    float loopCounter= stof(arg2[2]);


    // print to user the IEEE bit representation using the objects
    BitsetFloat bound_bit(loopBound);
    BitsetFloat counter_bit(loopCounter);

    cout<<"Loop bound:   ";
    bound_bit.PrintBits();
    cout<< endl;

    cout<<"Loop counter: ";
    counter_bit.PrintBits();
    cout<<endl;

    cout<<endl;

    // Calculate the threshold and print if overflow occurred to user
    float threshold = CalcThreshold(loopCounter);

    // if-else statement to check overflow by checking if threshold is less than bound
    if (threshold< loopBound){

        BitsetFloat bit(threshold);
        // print to user
        cout<<"Warning: Possible overflow!" << endl;
        cout<<"Overflow threshold:"<<endl;
        cout<<"        "<<threshold<<endl;
        cout<<"        ";
        bit.PrintBits();
        cout<<endl;

    } else {
        // print no overflow if threshold is larger than the bound
        cout<<"There is no overflow!"<<endl;

    }


    return 0;
}
