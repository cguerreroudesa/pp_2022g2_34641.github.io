#Archivos del programa
A continuación, se procederá a explicar las funciones que se desarrollan en los archivos.

#1. City.cpp
En esta sección se encuentran los métodos de la clase City
##City()
El constructor de la clase City recibe y guarda en sus atributos el nombre de la ciudad, sus coordenadas en el eje x y sus coordenadas en el eje y.

```cpp
City::City(std::string name, int x, int y){
    x_=x;
    y_=y;
    name_=name;
}
```
##getx()
Devuelve el valor del atributo x, es decir, las coordenadas en el eje x de la ciudad en cuestión.

```cpp
int City::getx(){
    return x_;
}
```
##gety()
Devuelve el valor del atributo y, es decir, las coordenadas en el eje y de la ciudad en cuestión.

```cpp
int City::gety(){
    return y_;
}
```
##getname()
Devuelve el valor del atributo name, es decir, el nombre de la ciudad en cuestión.

```cpp
std::string City::getname(){
    return name_;
}
```
##distanceTo()
Calcula la distancia entre dos ciudades. Por ejemplo, si yo quiero saber la distancia entre a y b ejecutaria la función de la siguiente manera: ` a.distanceTo(&b) `

```cpp
float City::DistanceTo( City* b){
    float xDis= abs(x_-b->getx());
    float yDis= abs(y_-b->gety());
    float distance= sqrt(pow(xDis, 2)+pow(yDis, 2));
    return distance;
}
```
#Lectura.cpp
En esta sección se encuentran los métodos de la clase City
##open()
La función open recibe el nombre de un archivo como string. Recorre cada línea del archivo, omitiendo aquellas que comiencen con #. En primer lugar, de cada línea leída se verifica en que posiciones se encuentran los separadores (espacio, coma o tabulación) y el largo de la línea. En segundo lugar, se calcula y se guarda en determinadas variables los datos de las ciudades: nombre, coordenadas en el eje x y coordenadas en el eje y, en el respectivo orden. Por último, se crea una ciudad con los parámetros obtenidos del archivo agregándola en un vector de ciudades. Esto se repetirá con todas las líneas del archivo, hasta que llegue al final u ocurra un error. Al finalizar el ciclo de lectura, el archivo se cierra y la función devuelve el vector de ciudades.

```cpp
std::vector<City> File::open(std::string arc){
    std::ifstream myfile(arc);
    while(getline(myfile, linea_)){
        if (linea_[0]!= '#'){
            first_ =linea_.find_first_of(" ,");
            last_= linea_.find_last_of(" ,");
            size_= linea_.size();
            std::string name = linea_.substr(0, first_); 
            std::string x=linea_.substr(first_+1, last_-(first_+1));
            std::string y=linea_.substr(last_+1, size_-last_);
            City city(name, stoi(x), stoi(y));
            cities.emplace_back(city);
        }
    }
    myfile.close();
    return cities;
}
```