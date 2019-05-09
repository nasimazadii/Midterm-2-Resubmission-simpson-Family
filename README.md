# Midterm-2-Resubmission-simpson-Family
//The code compiles, but unfortunately encountered an ‘Unexpected Exception handling.

#include<iostream>
#include<string>
#include<vector>

using namespace std;

class Parent;
class Child;
//void printInfo(Human hum);
class Human
{
private:

	Human();
	string name;
	int age;
	char sex;
protected:

	Human(string n, int a, char s)
	{
		name = n;
		age = a;
		sex = s;
	}
	virtual ~Human();
public:
	 string getName() const
	{
		return name;
	}
	int getAge() const
	{
		return age;
	}
	char getSex()
	{
		return sex;
	}
	void setSex(char ss)
	{
		sex = ss;
	}
	void setAge(int aa)
	{
		age = aa;
	}
	void setName(string nn)
	{
		name = nn;
	}

};
class Child : public Human
{
private:
	string momName, dadName;
	int allowance;
	Child();
public:
	Child(string n, int a, char s, string mn, string dn) :Human(n, a, s)
	{
		allowance = 0;
		momName = mn;
		dadName = dn;

	}
	int getAllowance() const
	{
		return allowance;
	}
	void printParent()
	{
		cout << "parents are:" << momName << " " << dadName << endl;
	}
	friend class allowanceAid;
	//friend void Parent:: setChildAllowance(int , Child );
	~Child() { delete this; Human :: ~Human();}
};
class allowanceAid
{
public:
	void changeAllowance(Child,int);
};
void allowanceAid::changeAllowance(Child c, int a)
{
	c.allowance = a;
}
class Parent : public Human
{
private:
	vector<string> children;
	Parent();
public:
	Parent(string n, int a, char s) : Human(n, a, s)
	{}
	void printChild()
	{
		for (int i = 0; i < children.size(); i++)
		{
			cout << children.at(i) << " " << endl;
		}
	}
	void setChild(Child *c);

	void setChildAllowance(int a, Child b);
	~Parent() { delete this;
	Human :: ~Human();
	}
	
};
void Parent:: setChild (Child *c)
{
	children.push_back(c->getName());
}
void Parent::setChildAllowance(int a, Child b)
{
	int childexists = 0;
	for (int i = 0; i < children.size(); i++)
	{
		if (children.at(i) == b.getName())
		{
			childexists = 1;
			break;
		}
	}
	if (childexists)
	{
		allowanceAid t;
		t.changeAllowance(b, a);
		//b.allowance = a; //why not????
	}
	else
	{	
		//cout << b.getName << "is not a child of him." << endl;
	}
}
Human::~Human() {delete this; }
//****main method:
void printInfo(Human *hum)
{
	cout << "Name:" << hum->getName() << endl;
	cout << "Age:" << hum->getAge() << endl;
	cout << "Sex:" << hum-> getSex() << endl;


}
 
int main()
{
	
	Parent  dad =  Parent("Homer", 36, 'M');
	Parent  mom =  Parent("March", 34, 'F');
	Child  liza =  Child ("Liza", 12, 'F',"March","Homer");
	Child  bart =  Child("Bart", 10, 'M', "March", "Homer");
	Child  maggie =  Child("Maggie", 3, 'F', "March", "Homer");
	dad.setChild(&bart);
	dad.setChild(&liza);
	dad.setChild(&maggie);
	mom.setChild(&bart);
	mom.setChild(&liza);
	mom.setChild(&maggie);
	cout << "bart's allowance was: " << bart.getAllowance() << endl;
	dad.setChildAllowance(5, bart);
	cout << "bart's allowance is: " << bart.getAllowance() << endl;
	bart.printParent();
	
	printInfo(&mom);
	printInfo(&liza);

	int holdconsole;
	cin >> holdconsole;
	return 0;


}
