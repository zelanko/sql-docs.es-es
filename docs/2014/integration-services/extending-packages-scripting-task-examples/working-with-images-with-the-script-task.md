---
title: Trabajar con imágenes con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4529ded6049327261ac92a76cc9861b7cec7dd61
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204585"
---
# <a name="working-with-images-with-the-script-task"></a>Trabajar con imágenes con la tarea Script
  Una base de datos de productos o usuarios suele incluir imágenes además de datos de texto y numéricos. El espacio de nombres `System.Drawing` de Microsoft .NET Framework proporciona clases para manipular las imágenes.  
  
 [Ejemplo 1: Convertir las imágenes al formato JPEG](#example1)  
  
 [Ejemplo 2: Crear y guardar las imágenes en miniatura](#example2)  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="example1"></a> Ejemplo 1: Descripción: convertir las imágenes al formato JPEG  
 En el ejemplo siguiente se abre un archivo de imagen especificado por una variable y se guarda como un archivo JPEG comprimido mediante un codificador. El código para recuperar la información del codificador se encapsula en una función privada.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Para configurar este ejemplo de la tarea Script para su uso con un archivo de imagen único  
  
1.  Cree una variable de cadena denominada `CurrentImageFile` y establezca el valor en la ruta de acceso y nombre de un archivo de imagen existente.  
  
2.  En el **Script** página de la **Editor de la tarea Script**, agregar el `CurrentImageFile` variable a la `ReadOnlyVariables` propiedad.  
  
3.  En el proyecto de script, establezca una referencia al espacio de nombres `System.Drawing`.  
  
4.  En el código, utilice las instrucciones `Imports` para importar los espacios de nombres `System.Drawing` y `System.IO`.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Para configurar este ejemplo de la tarea Script para su uso con varios archivos de imagen  
  
1.  Coloque la tarea Script dentro de un contenedor de bucles Foreach.  
  
2.  En la página **Colección** del **Editor de bucles Para cada uno**, seleccione como enumerador el **Enumerador de archivos Para cada uno** y especifique la ruta de acceso y la máscara de archivo de los archivos de código fuente, como "*.bmp".  
  
3.  En la página **Asignaciones de variables**, asigne la variable `CurrentImageFile` al índice 0. Esta variable pasa el nombre de archivo actual a la tarea Script de cada iteración del enumerador.  
  
    > [!NOTE]  
    >  Estos pasos son adicionales a los enumerados en el procedimiento para el uso con un archivo de imagen único.  
  
### <a name="example-1-code"></a>Código de ejemplo 1  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a> Ejemplo 2: Descripción: crear y guardar las imágenes en miniatura  
 En el ejemplo siguiente se abre un archivo de imagen especificado por una variable, se crea una miniatura de la imagen a la vez que se mantiene una relación de aspecto constante y se guarda la miniatura con un nombre de archivo modificado. El código que calcula el alto y ancho de la miniatura a la vez que mantiene una relación de aspecto constante se encapsula en una subrutina privada.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Para configurar este ejemplo de la tarea Script para su uso con un archivo de imagen único  
  
1.  Cree una variable de cadena denominada `CurrentImageFile` y establezca el valor en la ruta de acceso y nombre de un archivo de imagen existente.  
  
2.  Cree también la variable entera `MaxThumbSize` y asígnela un valor en píxeles, como 100.  
  
3.  En el **Script** página de la **Editor de la tarea Script**, agregue ambas variables a la `ReadOnlyVariables` propiedad.  
  
4.  En el proyecto de script, establezca una referencia al espacio de nombres `System.Drawing`.  
  
5.  En el código, utilice las instrucciones `Imports` para importar los espacios de nombres `System.Drawing` y `System.IO`.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Para configurar este ejemplo de la tarea Script para su uso con varios archivos de imagen  
  
1.  Coloque la tarea Script dentro de un contenedor de bucles Foreach.  
  
2.  En la página **Colección** del **Editor de bucles Para cada uno**, seleccione como **Enumerador** el **Enumerador de archivos Para cada uno** y especifique la ruta de acceso y la máscara de archivo de los archivos de código fuente, como "*.jpg".  
  
3.  En la página **Asignaciones de variables**, asigne la variable `CurrentImageFile` al índice 0. Esta variable pasa el nombre de archivo actual a la tarea Script de cada iteración del enumerador.  
  
    > [!NOTE]  
    >  Estos pasos son adicionales a los enumerados en el procedimiento para el uso con un archivo de imagen único.  
  
### <a name="example-2-code"></a>Código de ejemplo 2  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
