#include <iostream>
#include <string>
#include <map>
#include <tuple>


class University
{
private:
    std::string name;

public:
    //University(std::string unam):name(unam){};
    std::string postponed;
    int postponed_period;
    std::string sub;
   virtual void routine()
    {
        std::cout << "Enter your subject name:" << std::endl;

        std::cin >> sub;
        std::multimap<std::string, std::tuple<std::string, int>> week;
        week.insert(std::make_pair("Math", std::make_tuple("Sunday", 1)));
        week.insert(std::make_pair("OOP", std::make_tuple("Sunday", 2)));
        week.insert(std::make_pair("DSA", std::make_tuple("Sunday", 3)));
        week.insert(std::make_pair("EEE", std::make_tuple("Monday", 1)));
        week.insert(std::make_pair("Math", std::make_tuple("Monday", 2)));
        week.insert(std::make_pair("OOP", std::make_tuple("Tuesday", 1)));
        week.insert(std::make_pair("DSA", std::make_tuple("Tuesday", 2)));
        week.insert(std::make_pair("EEE", std::make_tuple("Wednesday", 1)));
        week.insert(std::make_pair("OOP", std::make_tuple("Wednesday", 2)));
        week.insert(std::make_pair("DSA", std::make_tuple("Thursday", 1)));
        week.insert(std::make_pair("Math", std::make_tuple("Thursday", 3)));
        week.insert(std::make_pair("OOP", std::make_tuple("Thursday", 2)));
        week.insert(std::make_pair("EEE", std::make_tuple("Thursday", 4)));

        std::cout << "You have your class on these days:" << std::endl;
        auto range = week.equal_range(sub);
        for (auto it = range.first; it != range.second; ++it)
        {
            std::cout << "Subject: " << it->first << ", Day: " << std::get<0>(it->second) << ", Period: " << std::get<1>(it->second) << std::endl;
        }
        std::cout<<"Give the information of cancellation :"<<std::endl;
        std::string ch;
        int t;
        std::cin>>ch>>t;
        postponed_period=t;
        postponed=ch;
    }
    void cancelled()
    {
        std::cout<<postponed<<std::endl;
        std::cout<<postponed_period<<std::endl;
    }
    void tsub(){std::cout<<sub;}

};

class Teacher : public University
{
private:
    std::string Tnam;
    std::string Subject;
    int pnum;
public:
    Teacher(std::string name,std::string s,int n):Tnam(name),Subject(s),pnum(n){};

    void routine(){University::routine();}
    friend void favourite_student();
    std::string stuf;
};
void favourite_student(Teacher &t){std::cout<<"Who is your favourite student"<<std::endl;
std::cin>>t.stuf;}

class CR : public University
{
private:
    std::string name;
    std::string Dep;
    int roll;

public:
      int date,month,year;
    CR(std::string nam,std::string dep,int r):name(nam),Dep(dep),roll(r)
    {
      std::cout<<"Hey CR ! Give the CT Date"<<std::endl;

      std::cin>>date>>month>>year;

    }
    void note(){std::cout<<date<<"-"<<month<<"-"<<year<<std::endl;}
    void CT(){std::cout<<Dep<<" department on "<<date<<"-"<<month<<"-"<<year<<std::endl;}
};



class Students : public CR,public Teacher
{
private:
    std::string YearandTerm;
public:
    friend void notice();

};

void notice()
{
    std::cout<<"We have a CT - "<<std::endl;
    void note();
    std::cout<<"We have a postponed class - "<<std::endl;
    void cancelled();

}

void operator<<(Teacher &t,CR &c )
{
    std::cout<<"Info about University - "<<std::endl;
    std::cout<<"Today ";t.tsub();std::cout<<"class has been postponed"<<std::endl;
    std::cout<<"CT will be taken of ";c.CT();
}



int main()
{
    University UNI;

   std::cout<<"Bonjour !"<<" Are you a teacher or CR ?"<<std::endl;

   std::string s;
   std::cin>>s;
   if(s=="Teacher")
   {
      std::cout<<"Enter your identity"<<std::endl;
      std::string nam,dep;
      int p;
      std::cin>>nam>>dep>>p;
      Teacher T(nam,dep,p);
      T.routine();

   }
   else if(s=="CR")
   {
       std::cout<<"Enter your identity"<<std::endl;
      std::string nam,dep;
      int p;
      std::cin>>nam>>dep>>p;
      CR c(nam,dep,p);


   }
   return 0;
    }
/*
  Discussion: In this project we have used almost all C++ features like inheritance , encapsulation , friend function , Diamond-problem ,
              constructor , virtual function , STL etc.But we did not use template because we don't need it in this project .
              We can further modify the program to increase it's usability .

  Reference : 1. Codes Beauty ( Saldina Nurak )
              2. ChatGpt
              3. Code::Blocks 20.03
              */
