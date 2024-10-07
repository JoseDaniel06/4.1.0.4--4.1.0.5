# Manual Funcional para la actualizaci�n de versiones ORM

# Introducci�n 
Para esta entrega se realiza un nuevo ejecutable, en este se arreglan dos bugs reportados anteriormente durante las pruebas realizadas.

![alt text](image.png)


# Instalar aplicaci�n
Para realizar la aplicaci�n de esta entrega se debe descargar el archivo .exe y reemplazarlo en la carpeta donde se tiene instalador el ORM, dejando solo el nuevo archivo.
![alt text](image-1.png)

Dar clic en reemplazar y se inicia el aplicativo con normalidad.


# Bugs corregidos en v4.1.0.5
Enero 3 2018 - Versi�n 4.1.0.5:   
�	Se ajusta manejo del nombre del archivo generado por tareas programadas, dado que si este nombre de archivo conten�a uno o varios caracteres �.� la funci�n de .NET que devuelve el nombre del archivo sin extensi�n solo tomaba hasta el primer punto y descartaba el resto del texto. Se incluye una mejora en el m�todo que devuelve la variable Archivo de la forma frmEditTareaPost.cs para remplazar la l�nea:

 ```Path.GetFileNameWithoutExtension(txtArchivo.Text)```

 por:

    string nomArch = txtArchivo.Text;
    if (txtArchivo.Text.ToUpper().EndsWith(".XLS") || txtArchivo.Text.ToUpper().EndsWith(".XLSX") || txtArchivo.Text.ToUpper().EndsWith(".CSV") ||
                            txtArchivo.Text.ToUpper().EndsWith(".RTF") || txtArchivo.Text.ToUpper().EndsWith(".PDF") || txtArchivo.Text.ToUpper().EndsWith(".TXT") ||
                            txtArchivo.Text.ToUpper().EndsWith(".HTML") || txtArchivo.Text.ToUpper().EndsWith(".XML"))
    {
        int index = nomArch.LastIndexOf('.');
        nomArch = index == -1 ? nomArch : nomArch.Substring(0, index);
    }
    return nomArch + "." + getArchivoExt();

 �	Se ajusta el manejo de la funci�n que devuelve el texto del query que se va a ejecutar sin los comentarios, antes de realizar el an�lisis de par�metros. Esta funcionalidad estaba descartando como comentarios en l�nea todas las apariciones de la cadena �--� sin importar si estos caracteres hac�an parte de una cadena o no (si estaban encerrados por comillas simples o dobles), lo cual estaba haciendo que todo el texto en la misma l�nea desde la ocurrencia de dicho �--� se eliminaba y e proceso de determinar los par�metros estaba fallando y el query estaba quedando con una sintaxis err�nea. Se ajusta la expresi�n regular que maneja este proceso de eliminado de comentarios para tener en cuenta la situaci�n anterior.