# AVANCE-03-2086234-Ximena-Rosales-Velazquez--
,,,
#include<iostream>
#include<conio.h>
#include<string.h>
#include<string>
#include<fstream>

using namespace std;

struct nodo{
    float precio_uni,iva,precio_total;
    string articulo, descripcion, caracteristicas, clasificacion, genero;
    int num_articulo,a_lanz,status=0;
    struct nodo *sgte;
};

void AgregarProducto(struct nodo *lista, int nart, string arti,int a_lan, string desc, string carac, string clasi, string gen, int pre){
     nodo *q=new nodo();
	 nodo *t=new nodo();
    t=lista;
    q->num_articulo=nart;
    q->articulo=arti;
    q->a_lanz=a_lan;
    q->descripcion=desc;
    q->caracteristicas=carac;
    q->clasificacion=clasi;
    q->genero=gen;
    q->precio_uni=pre;
    q->iva=pre*.16;
    q->precio_total=pre*1.16;
    q->status=1;
    if(lista->sgte!=NULL){
        while(t->sgte!=NULL){
            t=t->sgte;
        }
        q->sgte=NULL;
        t->sgte=q;
    }else{
        q->sgte=NULL;
        lista->sgte=q;
    }
    
}

void MostrarLista(struct nodo *lista){
	nodo *p=new nodo();
	p=lista->sgte;
	if(lista->sgte!=NULL){
		while(p!=NULL){
			cout<<"\tN. Articulo: "<<p->num_articulo<<endl;
			cout<<"\tArticulo: "<<p->articulo<<endl;
			cout<<"\tGenero: "<<p->genero<<endl;
			cout<<"\tClasificacion: "<<p->clasificacion<<endl;
			cout<<"\tFecha de lanzamiento: "<<p->a_lanz<<endl;
			cout<<"\tCaracteristicas: "<<p->caracteristicas<<endl;
			cout<<"\tDescripcion: "<<p->descripcion<<endl;
			cout<<"\tPrecio unitario: "<<p->precio_uni<<endl;
			cout<<"\tIVA: "<<p->iva<<endl;
			cout<<"\tPrecio Total: "<<p->precio_total<<endl;
			cout<<" "<<endl;	
        	p=p->sgte;
		}
	}else{
		cout<<"No hay productos."<<endl;
		cout<<" "<<endl;
	}
}

void ModificarArticulo(struct nodo *lista){
	nodo *p=new nodo();
	p=lista->sgte;
	int op, mod_art,resp=1,error=0;
	float price;
	string art, desc,carac;
	if(lista->sgte!=NULL){
		cout<<"Ingrese el numero del articulo a modificar."<<endl;
		cin>>mod_art;
   		while(p->num_articulo!=mod_art){
   			p=p->sgte;
		}
		if(p==NULL){
			cout<<"El numero de articulo no coincide con ningun articulo existente."<<endl;
			error=1;
		}		
		while(resp!=0 && error!=1){
			cout<<"Ingrese el dato a modificar."<<endl;
			cout<<"1. Articulo."<<endl;
			cout<<"2. Genero."<<endl;
			cout<<"3. Clasificacion."<<endl;
			cout<<"4. A. lanzamiento."<<endl;
			cout<<"5. Caracteristicas."<<endl;
			cout<<"6. Descripcion."<<endl;
			cout<<"7. Precio unitario."<<endl;
    		cin>>op;
    		switch(op){
    			case 1:
    				cout<<"Ingrese el nuevo nombre del articulo."<<endl;
    				cin>>art;
    				p->articulo=art;
    				break;
    			case 2:
    				cout<<"Ingrese el nuevo genero del articulo."<<endl;
    				cin>>p->genero;
    				break;
    			case 3:
    				cout<<"Ingrese la nueva clasificacion del articulo."<<endl;
    				cin>>p->clasificacion;
    				break;
    			case 4:
    				cout<<"Ingrese el nuevo a. de lanzamiento del articulo."<<endl;
    				cin>>p->a_lanz;
    				break;
    			case 5:
    				cout<<"Ingrese la nueva caracteristicas."<<endl;
    				cin>>carac;
    				p->caracteristicas=carac;
    				break;
    			case 6:
    				cout<<"Ingrese la nueva descripcion."<<endl;
    				cin>>desc;
    				p->descripcion=desc;
    				break;
    			case 7:
    				cout<<"Ingrese el nuevo precio base."<<endl;
    				cin>>price;
    				p->precio_uni=price;
    				p->iva=price*(.16);
    				p->precio_total=price+p->iva;
    				break;
    			default :
    				cout<<"Opcion no valida."<<endl;
    				break;
				}
				do{
					cout<<"\tDesea seguir modificando el articulo?"<<endl;
					cout<<"0. No, salir."<<endl;
					cout<<"1. Si."<<endl;
					cin>>resp;
				}while(resp!=0 && resp!=1);
			}
	}else{
		cout<<"No hay productos."<<endl;
		cout<<" "<<endl;
	}
    
}

void EliminarArticulo(struct nodo *lista){
	nodo *p=new nodo();
	p=lista->sgte;
	nodo *t=new nodo();
	t->sgte=p;
	int eli_art;
    if(lista->sgte!=NULL){
    	cout<<"Ingrese el numero del articulo a eliminar."<<endl;
    	cin>>eli_art;
    	while(p->num_articulo!=eli_art){
    		p=p->sgte;
		}
		if(p==NULL){
			cout<<"El numero de articulo no coincide con ningun articulo existente."<<endl;
		}
		if(p!=NULL){
			t->sgte=p->sgte;
			if(lista->sgte==p && p->sgte==NULL){
				lista->sgte=NULL;
			}
			delete(p);
		}
		
		
	}else{
		cout<<"No hay productos."<<endl;
		cout<<" "<<endl;
	}
}

int main(){
	nodo *ListaP=new nodo();
    ListaP->sgte=NULL;
   int opcion, n_art,resp=1,a_lan;
   float price;
   string art, desc,carac, clasi, gen;
	do{
		cout << "\t Tienda de videojuegos: PACMAN \n";//nombre de la tienda de videojuegos
		cout <<" 1.-Agregar articulo\n 2.-Modificar articulo\n 3.-Eliminar articulo\n 4.-Lista de articulos\n 5.-Limpiar pantalla\n 6.-Salir\n";//opciones que deberian salir en el menu;
		cin >>opcion ;
		
		switch (opcion)	
		{
		    case 1: //Agregar articulo
			    cout <<"Ingrese el numero del articulo: \n";
			    cin>>n_art;
			    cout<<endl<<"Ingrese el nombre del articulo: \n";
			    cin.ignore();
			    getline(cin, art);
			    cout<<endl<<"Ingrese el genero del articulo: \n";
			    cin.ignore();
			    getline(cin, gen);
			    cout<<endl<<"Ingrese el a de lanzamiento del articulo: \n";
			    cin>>a_lan;
			    cout<<endl<< "Ingrese la descripcion del articulo: \n";
			    cin.ignore();
			    getline(cin, desc);
			    cout<<endl<<"Ingrese las caracteristicas del articulo: \n";
			    cin.ignore();
			    getline(cin, carac);
			    cout<<endl<<"Ingrese la clasificacion del articulo: \n";
			    cin.ignore();
			    getline(cin, clasi);
			    cout<<endl<<"Ingrese el precio base del articulo: \n";
			    cin >>price;
			    cout<<" "<<endl;
			    AgregarProducto(ListaP,n_art,art,a_lan,desc,carac,clasi,gen,price);
			    break;
		    case 2: //Modificar articulo
		    	ModificarArticulo(ListaP); 
		    break;
		    case 3: //Eliminar articulo
		        EliminarArticulo(ListaP);
		    break;
		    case 4: //Mostrar lista
		    	MostrarLista(ListaP);
		    break;
		    case 5: //Limpiar pantalla
		        system("cls");
		    break;
		    case 6: //Salir
			    do{
					cout<<"\tDesea salir del programa?"<<endl;
					cout<<"1. No."<<endl;
					cout<<"0. Si, salir."<<endl;
					cin>>resp;
				}while(resp!=0&&resp!=1);
			    if(resp==0){
					cout<< "Gracias por su compra\n";
				}	
			    break;	
		    default:
		    	cout<<"Ingrese una opcion correcta\n"; //Por si se equivoca la persona, volver al menu principal
		}
		
		}while(resp!=0);
		    
}
