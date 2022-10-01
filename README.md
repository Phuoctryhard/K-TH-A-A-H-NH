/*Kế thừa – đa hình
OPP 1 [Kế thừa - Đa hình]. Bài 1. Kế thừa lớp Person
•	Problem
•	Submissions
•	Leaderboard
•	Discussions
Xây dựng lớp Person với các thuộc tính : Tên (xâu kí tự không quá 100 kí tự), ngày sinh, địa chỉ và các hàm khởi tạo không tham số (gán các trường là xâu rỗng) và hàm khởi tạo đầy đủ tham số, phương thức toString để trả về thông tin. Lớp Student kế thừa từ lớp Person và có thêm thuộc tính là mã sinh viên, GPA và lớp, ghi đè phương thức toString. Nhập danh sách sinh viên từ bàn phím và in ra màn hình danh sách sinh viên trong đó tên được chuẩn hóa và ngày sinh đưa về đúng chuẩn dd/mm/yyyy.
Input Format
Dòng 1 là N : số lượng sinh viên. Các dòng tiếp theo là thông tin sinh viên, mỗi sinh viên được mô tả bằng 5 dòng : Tên, ngày sinh, địa chỉ, lớp, gpa.
Constraints
1<=N<=1000;
Output Format
In ra danh sách sinh viên sau khi được chuẩn hóa, mã sinh viên tăng tự động từ 0001. Các thông tin viết cách nhau một dấu cách, điểm GPA in ra với 2 số sau dấu phẩy.
Sample Input 0
7
Nguyen AnH MaNH
27/8/2004
Nam Dinh
CNTT2
2.70
pham Phuong TuaN
21/9/2004
Nam Dinh
CNTT1
2.70
Vu Ngoc NAM
7/9/2004
Nam Dinh
CNTT2
3.05
Vu AnH LoNG
17/12/2004Ha Noi
CNTT1
2.80
Nguyen Phuong NAM
23/6/2004Ha Nam
HTTT3
2.80
Luong AnH NAM
16/1/2004
Thai Binh
DTVT1
2.80
Nguyen Phuong HaI
14/1/2004
Nam Dinh
DTVT1
3.05
Sample Output 0
0001 Nguyen Anh Manh 27/08/2004 Nam Dinh CNTT2 2.70
0002 Pham Phuong Tuan 21/09/2004 Nam Dinh CNTT1 2.70
0003 Vu Ngoc Nam 07/09/2004 Nam Dinh CNTT2 3.05
0004 Vu Anh Long 17/12/2004 Ha Noi CNTT1 2.80
0005 Nguyen Phuong Nam 23/06/2004 Ha Nam HTTT3 2.80
0006 Luong Anh Nam 16/01/2004 Thai Binh DTVT1 2.80
0007 Nguyen Phuong Hai 14/01/2004 Nam Dinh DTVT1 3.05
+ hàm chuẩn hóa ngày sinh viết trong lớp cha luôn để vài bữa kế thừa cho êm .

*/
#include<bits/stdc++.h>
using namespace std;
class Person{
    private:
    string ten,ngaysinh,diachi;
    public:
        Person(){
            ten ="";ngaysinh ="";diachi="";
            
        }
        Person(string ten,string ngaysinh,string diachi){
            this->ten = ten ;
            this->ngaysinh = ngaysinh ;
            this->diachi = diachi;
        }
        // to string de tra ve thong tin 
        /*string toString(){
            string res= ten +" "+ ngaysinh +" "+ diachi;
            return res;
        */
        
        void toString(){
            string res= ten +" "+ ngaysinh +" "+ diachi;
            cout<<res<<' ';    
        }
        void chuanhoa(){
            string res="";
            stringstream ss(ten);
            string tmp ;
            while(ss>>tmp){
                res += toupper(tmp[0]);
                for(int i=1;i<tmp.size(); i++){
                    res += tolower(tmp[i]);
                    
                }
                res +=" ";
            }
            res.pop_back(); // xoa di ki tu cuoi cung;
            this->ten = res;
            if(this->ngaysinh[1]=='/')this->ngaysinh ="0"+this->ngaysinh;
            if( this->ngaysinh[4] == '/') this->ngaysinh.insert(3,"0");
            
        }
};

class Student:public Person{
    private:
    string masinhvien,lop;
    double gpa;
     public :
     Student(string ten, string ngaysinh,string diachi, int masinhvien,double gpa, string lop):Person(ten,ngaysinh,diachi){
         
         this->masinhvien=to_string(masinhvien);
         while(this->masinhvien.size()<4) this->masinhvien="0" + this->masinhvien;        
         this->gpa = gpa;
         this->lop=lop;
 }
//     string toString(){ // do dime co kieu tra ve nen phai cout 
//         return this->masinhvien +" "+Person:toString()
    void toString(){
        cout<<this->masinhvien<<' ';
        Person::toString();
        cout<<this->lop<<' '<<fixed<<setprecision(2)<<this->gpa<<endl;
     }
};
int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin.ignore();
        string ten;
        getline(cin,ten);
        string s;
        getline(cin,s);
        string ns="",dc="";
        int j=0;
        while(!isalpha(s[j])){
            ns+=s[j];
            ++j;
        }
        while(j<s.size()){
            dc+=s[j];++j;
        }
        string lop;
        getline(cin,lop);
        double gpa;
        cin>>gpa;
        Student st(ten,ns,dc,i+1,gpa,lop);
        st.chuanhoa();
        st.toString();
    }
}
