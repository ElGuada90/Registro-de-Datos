# Registro-de-Datos
Registro de Datos
from tkinter import messagebox
import customtkinter
from PIL import Image


'''class EntryFrame(customtkinter.CTkFrame):
    def __init__(self, master):
        super().__init__(master)
        self.grid_columnconfigure((0,1,), weight=1)
        
          
        self.title = customtkinter.CTkLabel(self, text='LOGIN',fg_color=('light gray',"gray30"), text_color='gray', corner_radius=6,
                                            font=customtkinter.CTkFont(size=18, weight="bold"))
        self.title.grid(row=0, column=0, padx=10, pady=(10, 0), columnspan=2, sticky="ew")
        self.entry_usuario = customtkinter.CTkEntry(self, placeholder_text="NOMBRE DE USUARIO", width=50, height=50)
        self.entry_usuario.grid(row=1, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')
        self.entry_contraseña = customtkinter.CTkEntry(self, placeholder_text="COTRASEÑA", show='*', width=50, height= 50)
        self.entry_contraseña.grid(row=2, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')'''

'''class App(customtkinter.CTk):
    def __init__(self):
        super().__init__()'''
        
logo = customtkinter.CTkImage(dark_image=Image.open('C:\\Users\\jguadamuz\\Videos\\imagen.PNG'), size =(280, 100)) 
 
ventana_login=customtkinter.CTk()        
ventana_login.title('My App')
ventana_login.geometry('520x500+525+100')
ventana_login.grid_columnconfigure((0,1,), weight=1)
        
frame = customtkinter.CTkFrame(ventana_login)
frame.grid(row=1, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')
frame.grid_columnconfigure(0, weight=1)
label_Login = customtkinter.CTkLabel(frame, text='LOGIN',fg_color=('light gray',"gray30"), text_color='gray', corner_radius=6,
                                            font=customtkinter.CTkFont(size=18, weight="bold"))
label_Login.grid(row=0, column=0, padx=10, pady=(10, 0), columnspan=2, sticky="ew")
entry_usuario = customtkinter.CTkEntry(frame, placeholder_text="NOMBRE DE USUARIO", width=50, height=50)
entry_usuario.grid(row=1, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')
entry_contraseña = customtkinter.CTkEntry(frame, placeholder_text="COTRASEÑA", show='*', width=50, height= 50)
entry_contraseña.grid(row=2, column=0, padx=20, pady= 20, columnspan=2, sticky='nsew')

    
def button_callback():
        ventana_login.destroy()        
button1 = customtkinter.CTkButton(ventana_login, text="", bg_color='white', fg_color='white', width=50, height=50, image=logo, command=button_callback)
button1.grid(row=0, column=0, padx=20, pady=20, columnspan=2, sticky='ew')
     
 
def inicio_sesion():
      
    usuario = entry_usuario.get()
    contraseña = entry_contraseña.get()

    # Verificar nombre de usuario y contraseña
    if  usuario == "admin" and contraseña == "admin123":
        messagebox.showinfo("Inicio de sesión", "Inicio de sesión exitoso")
        
        entry_usuario.delete(0, customtkinter.END)
        entry_contraseña.delete(0, customtkinter.END)
        # Cerrar la ventana de inicio de sesión y mostrar la ventana principal      
        ventana_login.destroy()
        ventana_principal=customtkinter.CTk()
        ventana_principal.geometry('1280x720+160+50')
        ventana_principal.title('Operación de Carga')  
        ventana_principal.grid_columnconfigure(0, weight=1)
        ventana_principal.grid_rowconfigure(0, weight=1)
        
   
        def imprimir_datos(event):
            
            datos = entry_Registro.get()  # Obtener el código escaneado en el CTkEntry
            textbox_datos.insert(customtkinter.END + "-1c", datos + " ")  # Agregar el código al CTkTextbox
            entry_Registro.delete(0, customtkinter.END) 
            textbox_datos.insert(customtkinter.END, "\n") 
            # Limpiar el CTkEntry después de registrar el código de barras
              #entry_Registro.delete(0, customtkinter.END)
            label_Show.configure(text=datos)

        frame1= customtkinter.CTkFrame(ventana_principal, 
                               width=1000,
                               height=100,
                               fg_color='white')
        frame1.grid(row=0, column=0, padx=20, pady=(0,20), sticky='nsew')
        frame1.grid_columnconfigure((0, 1), weight=1)
        frame2= customtkinter.CTkFrame(frame1, 
                               width=1000,
                               height=100,
                               fg_color='white')
        frame2.grid(row=3, column=0, padx=20, pady=(0,20), columnspan=2, sticky='nsew')
        frame2.grid_columnconfigure((0, 1, 2, 3, 5, 6, 7, 8, 9, 10), weight=1)
        logo_Principal = customtkinter.CTkImage(light_image=Image.open('C:\\Users\\jguadamuz\\Videos\\imagen.PNG'), size =(280, 100)) 
        label_logo = customtkinter.CTkLabel(frame1,
                                  image=logo_Principal, 
                                  text='',
                                  width=280,
                                  height=100,
                                  font=customtkinter.CTkFont(size=24, weight="bold"),
                                  bg_color='white',
                                  fg_color='white')
        label_logo.grid(row=0, column=0, padx=20, pady=(0,20), columnspan=2, sticky='we')
        Label_Title = customtkinter.CTkLabel(frame1, text='OPERACIONES DE CARGA DE CAMION',
                                           width=50,
                                           height=50,
                                           fg_color='light gray',
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
        entry_Registro.bind('<Return>', imprimir_datos) #'<KeyRelease>'
        label_Show = customtkinter.CTkLabel(frame1,
                                           text='',
                                           width=350,
                                           height=25,
                                           font=customtkinter.CTkFont(size=40, weight="bold"))
        label_Show.grid(row=0, column=0, padx=20, pady=(0, 20), sticky='w')
        boton_inicio = customtkinter.CTkButton(frame2, text='Iniciar Carga',
                                           width=100,
                                           height=25,
                                           text_color='white',
                                           fg_color='light blue',
                                            corner_radius=10,
                                           font=customtkinter.CTkFont(size=12, weight="bold"))
        boton_inicio.grid(row=4, column=1, padx=20, pady=(0, 20), sticky='we')
        textbox_datos = customtkinter.CTkTextbox(frame2)
        textbox_datos.grid(row=5, column=0, padx=20, pady=(0, 20), columnspan=11, sticky='we')  

    
        ventana_principal.mainloop()     
            
        
    else:
        messagebox.showerror("Inicio de sesión", "Nombre de usuario o contraseña incorrectos")
        
button2 = customtkinter.CTkButton(ventana_login, text="INICIAR SESION", width=50, height=50, 
                                              font=customtkinter.CTkFont(size=18, weight="bold"), 
                                              command=inicio_sesion)
button2.grid(row=3, column=0, padx=20, pady=20, columnspan=2, sticky='ew')            

ventana_login.mainloop() 
 
