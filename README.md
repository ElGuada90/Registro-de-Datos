import datetime
import mysql.connector
from tkinter import messagebox
import customtkinter
from PIL import Image
#import openpyxl
ID=None
def abrir_ventana_principal(Usuario):
    global ID    
    customtkinter.set_appearance_mode("light")
    ventana_principal=customtkinter.CTk()
    ventana_principal.geometry('1280x720+160+50')
    ventana_principal.title('Operación de Carga')  
    ventana_principal.grid_columnconfigure(0, weight=1)
    ventana_principal.grid_rowconfigure(0, weight=1)
    #Widgets de ventana principal    
    frame1= customtkinter.CTkFrame(ventana_principal, 
                               width=1000,
                               height=100,
                               fg_color='white')
    frame1.grid(row=0, column=0, padx=20, pady=(5,5), sticky='nsew')
    frame1.grid_columnconfigure((0, 1), weight=1)
    frame2= customtkinter.CTkFrame(frame1, 
                               width=1000,
                               height=100,
                               fg_color='white')
    frame2.grid(row=3, column=0, padx=20, pady=(0,20), columnspan=2, sticky='nsew')
    frame2.grid_columnconfigure((0, 1, 2, 3, 5, 6, 7, 8, 9, 10), weight=1)
    logo_Principal = customtkinter.CTkImage(light_image=Image.open('C:\\Users\\jguadamuz\\Documents\\PROYECTOS PY\\iconos, del logo CSS.png'), size =(75, 75)) 
    label_Title = customtkinter.CTkLabel(frame1,
                                  #image=logo_Principal, 
                                  text='DESPACHOS',
                                  width=280,
                                  height=100,
                                  font=customtkinter.CTkFont(size=40, weight="bold"),
                                  bg_color='white',
                                  fg_color='white')
    label_Title.grid(row=0, column=0, padx=20, pady=(0,20), columnspan=2, sticky='we')
    label_logo = customtkinter.CTkLabel(frame1, text='', image=logo_Principal)
    label_logo.grid(row=0, column=0, padx=20, pady=20, columnspan=2, sticky='e')
    Label_Title = customtkinter.CTkLabel(frame1, text='PRODUCTIVIDAD OPERACIONES DE CARGA DE CAMION',
                                           width=50,
                                           height=50,
                                           fg_color='light blue',
                                           corner_radius=10,
                                           font=customtkinter.CTkFont(size=24, weight="bold"))
    Label_Title.grid(row=1, column=0, padx=20, pady=(0, 20), columnspan=11, sticky='we')
    entry_IDConductor = customtkinter.CTkEntry(frame2, placeholder_text='ID de Conductor',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_IDConductor.grid(row=2, column=0, padx=20, pady=(0, 20), sticky='nsew')
    entry_Placa = customtkinter.CTkEntry(frame2, placeholder_text='N° de Placa',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_Placa.grid(row=2, column=1, padx=20, pady=(0, 20), sticky='nsew')
    entry_Base = customtkinter.CTkEntry(frame2, placeholder_text='ID de Base',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_Base.grid(row=3, column=0, padx=20, pady=(0, 20), sticky='nsew')
    entry_Ubicacion = customtkinter.CTkEntry(frame2, placeholder_text='ID de Ubicación',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_Ubicacion.grid(row=3, column=1, padx=20, pady=(0, 20), sticky='nsew')
    entry_Transporte = customtkinter.CTkEntry(frame2, placeholder_text='Transportista',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_Transporte.grid(row=2, column=2, padx=20, pady=(0, 20), sticky='nsew')
    entry_Registro = customtkinter.CTkEntry(frame2, placeholder_text='Registro de LPN',
                                           width=150,
                                           height=25,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    entry_Registro.grid(row=4, column=0, padx=20, pady=(0, 20), sticky='nsew')
    label_Show = customtkinter.CTkLabel(frame1,
                                           text='',
                                           width=350,
                                           height=25,
                                           font=customtkinter.CTkFont(size=25, weight="bold"))
    label_Show.grid(row=0, column=0, padx=20, pady=(0, 20), sticky='w')
    label_Show.configure(text='Bienvenido, ' + Usuario)
    textbox_datos = customtkinter.CTkTextbox(frame2, height=350)
    textbox_datos.grid(row=5, column=0, padx=20, pady=(0, 20), columnspan=11, sticky='we')  
    def iniciar_tiempo():
        hora_inicio = datetime.datetime.now().strftime("%H:%M:%S")
        textbox_datos.insert(customtkinter.END, "Hora de inicio: " + hora_inicio + "\n")
    boton_inicio = customtkinter.CTkButton(frame2, text='Iniciar Carga',
                                           width=100,
                                           height=25,
                                           text_color='white',
                                           fg_color='blue',
                                           corner_radius=10,
                                           command=iniciar_tiempo,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    boton_inicio.grid(row=4, column=1, padx=20, pady=(0, 20), sticky='we')
    def detener_tiempo():
        global ID
        hora_cierre = datetime.datetime.now().strftime("%H:%M:%S")            
        textbox_datos.insert(customtkinter.END, "Hora de cierre: " + hora_cierre + "\n")
        # Establecer la conexión a la base de datos
        conexion = mysql.connector.connect(
        host="localhost",
        user="root",
        password="JGmay12345_.#",
        database="Despachos"
        )
        cursor = conexion.cursor()
        # Construir la consulta SQL para actualizar el registro
        consulta = "UPDATE productividad SET TCierre = %s WHERE id = %s"
        valores = (hora_cierre, ID)  # Asegúrate de tener el valor de id_registro
        cursor.execute(consulta, valores)
        conexion.commit()
    boton_STOP = customtkinter.CTkButton(frame2, text='Detener Carga',
                                           width=100,
                                           height=25,
                                           text_color='white',
                                           fg_color='blue',
                                           corner_radius=10,
                                           command=detener_tiempo,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
    boton_STOP.grid(row=4, column=2, padx=20, pady=(0, 20), sticky='we')
        
    def imprimir_datos(event):
        global ID 
        fecha = datetime.datetime.now()
        #usuario = entry_usuario.get()
        conductor = entry_IDConductor.get()
        camion = entry_Placa.get()
        base = entry_Base.get()
        puerta=entry_Ubicacion.get()
        transportista=entry_Transporte.get()
        lpn = entry_Registro.get()
        hora_inicio = datetime.datetime.now().strftime("%H:%M:%S")
        #hora_cierre = datetime.datetime.now().strftime("%H:%M:%S")
            
        # Conexión a la base de datos
        conexion = mysql.connector.connect(
        host="localhost",
        user="root",
        password="JGmay12345_.#",
        database="Despachos"
        )
        cursor = conexion.cursor()

    # Consulta para insertar registro de datos en la tabla productividad
        consulta = "INSERT INTO productividad (fecha, usuario, Base, TInicio) VALUES (%s, %s, %s, %s)"
        valores = (fecha, Usuario, base, hora_inicio)
        cursor.execute(consulta, valores)
        conexion.commit()
        ID=cursor.lastrowid     
        datos = f'Fecha: {fecha.strftime("%Y-%m-%d %H:%M:%S")}\'Usuario: {Usuario} \'Conductor: {conductor}\'Camión: {camion}\'Base: {base}\'Puerta: {puerta}\'Transportista: {transportista}\'LPN: {lpn}\n'
        textbox_datos.insert(customtkinter.END + "-1c", datos + "")  # Agregar el código al CTkTextbox
        entry_IDConductor.delete(0, customtkinter.END) 
        entry_Placa.delete(0, customtkinter.END) 
        entry_Base.delete(0, customtkinter.END)
        entry_Ubicacion.delete(0, customtkinter.END)  
        entry_Transporte.delete(0, customtkinter.END)
        entry_Registro.delete(0, customtkinter.END)  
        #textbox_datos.insert(customtkinter.END, "\n") 
        conexion.commit()
        # Limpiar el CTkEntry después de registrar el código de barras
        #label_Show.configure(text=datos)
    entry_IDConductor.bind('<Return>', imprimir_datos)
    entry_Placa.bind('<Return>', imprimir_datos)
    entry_Base.bind('<Return>', imprimir_datos)
    entry_Ubicacion.bind('<Return>', imprimir_datos)
    entry_Transporte.bind('<Return>', imprimir_datos)
    entry_Registro.bind('<Return>', imprimir_datos) #'<KeyRelease>'
    ventana_principal.mainloop() 
                         
def inicio_sesion():
    #INGRESO DE DATOS, USUARIO Y CONTRASEÑA  
    Usuario = entry_usuario.get()
    Contraseña = entry_contraseña.get()

  # Conexión a la base de datos
    conexion = mysql.connector.connect(
        host="localhost",
        user="root",
        password="",
        database=""
    )
    cursor = conexion.cursor()

    # Consulta para verificar el usuario y contraseña
    consulta = "SELECT * FROM usuarios WHERE Usuario = %s AND Contraseña = %s"
    valores = (Usuario, Contraseña)
    cursor.execute(consulta, valores)
    resultado = cursor.fetchone()
 
    # Verificar si el usuario y contraseña son válidos
    if resultado:
        messagebox.showinfo("Acceso correcto", "Bienvenido al sistema.")
        entry_usuario.delete(0, customtkinter.END)
        entry_contraseña.delete(0, customtkinter.END)
        # Cerrar la ventana de inicio de sesión y mostrar la ventana principal      
        ventana_login.destroy()
        abrir_ventana_principal(Usuario)
        
    else:
        messagebox.showerror("Acceso incorrecto", "Usuario o contraseña incorrectos.")

    # Cerrar la conexión y el cursor
    cursor.close()
    conexion.close()             
#CREAMOS LA VENTANA PARA EL LOGIN              
customtkinter.set_appearance_mode("light") 
ventana_login=customtkinter.CTk()        
ventana_login.title('My App')
ventana_login.geometry('520x480+525+100')
ventana_login.grid_columnconfigure((0,1), weight=1)
#Definimos una función, par que al hacer click en el boton del logo, se cierre la ventana del login.
def button_callback():
    ventana_login.destroy() 
#Creamos los widegets para cada objeto.
Logo = customtkinter.CTkImage(light_image=Image.open('C:\\Users\\jguadamuz\\Documents\\PROYECTOS PY\\iconos, del logo CSS.png'), size =(75, 75))        
logo = customtkinter.CTkButton(ventana_login, 
                            image=Logo,
                            text="",
                            text_color='blue',
                            font=customtkinter.CTkFont(family='Broadway', size=35, weight="bold"),
                            bg_color='transparent',
                            fg_color='transparent',  
                            command=button_callback)
logo.grid(row=0, column=0, padx=20, pady=20, columnspan=2, sticky='ew')        
frame = customtkinter.CTkFrame(ventana_login)
frame.grid(row=1, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')
frame.grid_columnconfigure(0, weight=1)
label_Login = customtkinter.CTkLabel(frame, text='LOGIN',fg_color=('light gray',"gray30"), text_color='gray', corner_radius=6,
                                            font=customtkinter.CTkFont(size=18, weight="bold"))
label_Login.grid(row=0, column=0, padx=20, pady=(10, 0), columnspan=2, sticky="ew")
entry_usuario = customtkinter.CTkEntry(frame, placeholder_text="NOMBRE DE USUARIO", width=50, height=50)
entry_usuario.grid(row=1, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')
entry_contraseña = customtkinter.CTkEntry(frame, placeholder_text="COTRASEÑA", show='*', width=50, height= 50)
entry_contraseña.grid(row=2, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')              
button_Login = customtkinter.CTkButton(ventana_login, text="INICIAR SESION", width=50, height=50, 
                                              font=customtkinter.CTkFont(size=18, weight="bold"), 
                                              command=inicio_sesion)
button_Login.grid(row=2, column=0, padx=20, pady=(5,5), columnspan=2, sticky='ew')            
#button_Login.bind('<Return>', imprimir_datos)

ventana_login.mainloop()
