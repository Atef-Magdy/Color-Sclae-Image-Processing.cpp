# Color-Sclae-Image-Processing.cpp
Image Processor (Using Library)(Color Scale) 

// FCI _ Programming 1 _ 2018 - Assignment 3
// Program Name: Color Scale Image Processor.cpp
// Last Modification Date: 6/4/2018
// Author: ATEF MAGDY
// Purpose: Image Processor

#include <iostream>
#include <cstring>
#include <cmath>
#include "bmplib.cpp"

using namespace std;

unsigned char image[SIZE][SIZE][RGB];
unsigned char flip[SIZE][SIZE][RGB];

void load();
void save();

void Black_White();
void FlipH();
void FlipV();
void DetectEdges();

int main()
{
    load();

    DetectEdges();

    save();

    return 0;
}

void load(){
   char imageFileName[100];
   cout << "Enter the source image file name: ";
   cin >> imageFileName;
   strcat (imageFileName, ".bmp");
   readRGBBMP(imageFileName, image);
}
void save(){
    char imageFileName[100];
   cout << "Enter the target image file name: ";
   cin >> imageFileName;
   strcat (imageFileName, ".bmp");
   writeRGBBMP(imageFileName, image);
}
void Black_White(){
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                if((image[i][j][0]+image[i][j][1]+image[i][j][2])>128*3){
                        image[i][j][0]=255;
                        image[i][j][1]=255;
                        image[i][j][2]=255;
                    }
                else {
                        image[i][j][0]=0;
                        image[i][j][1]=0;
                        image[i][j][2]=0;
                    }
        }}
}
void FlipH(){
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                for(int k=0 ; k<RGB ; ++k){
                flip[255-i][j][k]=image[i][j][k];
        }}}
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                for(int k=0 ; k<RGB ; ++k){
                image[i][j][k]=flip[i][j][k];
        }}}

}
void FlipV(){
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                for(int k=0 ; k<RGB ; ++k){
                flip[i][255-j][k]=image[i][j][k];
        }}}
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                for(int k=0 ; k<RGB ; ++k){
                image[i][j][k]=flip[i][j][k];
        }}}
}
void DetectEdges(){
    Black_White();
    for(int i=0 ; i<SIZE ; ++i){
        for(int j=0 ; j<SIZE ; ++j){
                for(int k=0 ; k<RGB ; ++k){
                    if((image[i][j][k]-image[i][j+1][k])>20 || (image[i][j][k]-image[i][j+1][k])<-20 ||
                        (image[i][j][k]-image[i+1][j][k])>20 || (image[i][j][k]-image[i+1][j][k])<-20)
                        image[i][j][k]=0;
                    else image[i][j][k]=255;
        }}}


}
