#include <bits/stdc++.h>
using namespace std;
class Car;
class Product {
protected:
    string name;
    double price;
public:
    Product(string name,double price) {
        this->name=name;
        this->price=price;
    }
    virtual ~Product()=default;
    double getPrice() const {
        return price;
    }
     string  getName()const {
        return name;
    }
    void setName(string n) {
        this->name=n;
    }
    void  setPrice(double  p)  {
        this->price=p;
    }
    virtual void Print () const {
        cout<<"Name of product:"<<name<<"\n";
        cout<<"Price:"<<price<<"$\n";
    }

};
enum Input{Open,Lock,Trunk};

class Key {
private:
    Car* car=nullptr;
    string code;
    Input input;

public:
    Key(Car* car,string const  &code, Input input) {
        this->car=car;
        this->code=code;
        this->input=input;
    }
    string getCode() const {
        return code;
    }
    void InputType(Input in);
    void setInput(Input in) {
        this->input=in;
    }
    void setCarCondition(Input in,string c) {
        if (code!=c) {
            cout<<"Wrong key!\n";
            return;
        }
        InputType(in);

    }
};
class Car:public Product {
private:

    string car_code;
    bool isLocked=false;
    bool trunkOpen=false;

public:
    vector<Product*> ProductsInTrunk;
    Car(const string   &name,double price,string car_code):Product(name,price) {
        this->car_code=car_code;
    }
    void setCode(string cc) {
        this->car_code=cc;
    }
    bool getTrunkCond() {
        return this->trunkOpen;
    }

    void Open() {
        cout<<getName()<<" is now opened!\n";
        this->isLocked=false;
    }
    void Lock() {
        cout<<getName()<<" is now locked\n";
        this->isLocked=true ;
    }
    void Trunk(){
    cout<<" Trunk is now open\n";
        this->trunkOpen=true;
    }
    void TakeOutOfTrunk(Product* p) {
        if (getTrunkCond()==false) {
            cout<<"Trunk is not open\n";
            return;
        }
        for (auto it = ProductsInTrunk.begin(); it != ProductsInTrunk.end(); ) {
            if (*it == p) {
                it = ProductsInTrunk.erase(it);
                return;
            }
            ++it;
        }
        cout<<"Product:"<<p->getName()<<"not found\n";
    }
    void AddToTrunk(Product *p) {
        if (!trunkOpen) {
            cout << "Cannot add product. Trunk is closed!\n";
            return;
        }
        ProductsInTrunk.push_back(p);
    }
    void PrintProd() {
        if (getTrunkCond()) {
            for (auto &p : ProductsInTrunk)
                cout << "Product: " << p->getName() << "\n";
        } else {
            cout << "Trunk is closed!\n";
        }
    }
    void Print() const override {
        cout << "Car: " << getName() << ", Price: " << getPrice() << "$\n";
    }

};
void Key::InputType(Input in) {
    setInput(in);
    switch (in) {
        case Open:
            car->Open();
            break;
        case Lock:
            car->Lock();
            break;
        case Trunk:
            car->Trunk();
            break;
        default:
            cout<<"Invalid input\n";
    }
}
template <typename T>
T* findCheapest(const vector<T*> &items) {
    if (items.empty())
        return nullptr;
     T* mini=items[0];
    for (auto &p:items)
         if(mini->getPrice()>p->getPrice())
             mini=p;
    return mini;
}

int main(){
    vector<Product*> products;
    vector<Car*> cars;
    vector<Key*> carKeys;
    products.push_back(new Product("Laptop", 1200));
    products.push_back(new Product("Phone", 800));
    products.push_back(new Product("Headphones", 150));
    cars.push_back(new Car("BMW", 30000, "X1"));
    cars.push_back(new Car("Audi", 25000, "A3"));
    cout<<"Cheapest product is: "<<findCheapest(products)->getName()
    <<" "<<findCheapest(products)->getPrice()<<"$\n";
    cout<<"Cheapest car is: "<<findCheapest(cars)->getName()
    <<" "<<findCheapest(cars)->getPrice()<<"$\n";
    for (auto c: cars) {
        carKeys.push_back(new Key(c, c->getName(), Open));
    }
    for (auto key : carKeys) {
        cout << "\nOpening car with key for " << key->getCode() << ":\n";
        key->setCarCondition(Open, key->getCode());   // unlock car
        key->setCarCondition(Trunk, key->getCode());  // open trunk
    }

    // Add products to first car trunk (BMW)
    Car* myCar = cars[0]; // BMW
    myCar->AddToTrunk(products[0]); // Laptop
    myCar->AddToTrunk(products[2]); // Headphones

    cout << "\nProducts in " << myCar->getName() << " trunk:\n";
    myCar->PrintProd();

    // Remove a product from trunk
    myCar->TakeOutOfTrunk(products[0]); // remove Laptop
    cout << "\nAfter removing Laptop:\n";
    myCar->PrintProd();

    //  Try to lock a car with wrong code
    cout << "\nAttempting to lock BMW with wrong key:\n";
    carKeys[0]->setCarCondition(Lock, "wrongcode");


    return 0;
}
