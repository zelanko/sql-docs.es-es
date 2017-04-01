---
title: "Buscar y ver informes con un explorador (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: edf4843a-2a0a-486f-be25-14a3c1c6bc72
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# Buscar y ver informes con un explorador (Generador de informes y SSRS)
  Puede utilizar cualquier explorador web compatible para ver un informe mediante una conexión directa a un servidor de informes. Cada informe dispone de una dirección URL en el servidor de informes. Puede escribir la dirección web de un informe para abrirlo por sí solo en una ventana del explorador de una aplicación web. El informe se abre en formato HTML e incluye la barra de herramientas de informe para que pueda navegar por las páginas o buscar valores de datos dentro del informe. Puede establecer parámetros en la dirección URL para ocultar la barra de herramientas o para seleccionar el formato de salida del informe.  
  
 La apertura de un informe a través de su dirección web es adecuada para verlo, pero no para administrarlo. No se puede tener acceso a las páginas de propiedades de un elemento ni a las páginas de definición de suscripciones. Debe utilizar el Administrador de informes o un sitio de SharePoint para esas tareas.  
  
 Si no conoce la dirección web de un informe, puede abrir la dirección web del servidor de informes y, a continuación, examinar la jerarquía de carpetas del servidor de informes para seleccionar el informe desea ver. El siguiente diagrama muestra una jerarquía de carpetas tal como aparecería en una ventana de explorador.  
  
 ![Carpetas en un explorador](../../reporting-services/report-builder/media/rs-browserfolder.GIF "Carpetas en un explorador")  
Carpetas en un explorador  
  
> [!NOTE]  
>  Si obtiene acceso a un informe desde un dispositivo de mano, deberá utilizar el explorador para abrir los informes. El Administrador de informes todavía no ofrece compatibilidad con este tipo de dispositivos.  
  
 Para obtener más información acerca de los tipos de exploradores que puede usar, vea el tema relativo a los tipos de exploradores admitidos por Reporting Services en la [documentación de Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) en los Libros en pantalla de SQL Server.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Navegar por las carpetas del servidor de informes en un explorador web  
 Puede utilizar un explorador web para navegar por las carpetas del servidor de informes y ejecutar informes. Los informes y los elementos se muestran en forma de vínculos en la jerarquía de carpetas. Para abrir un informe, un recurso o una carpeta, o ver el contenido de un origen de datos compartido, haga clic en estos vínculos. La navegación por la jerarquía de carpetas puede resultarle útil si desconoce la dirección URL de un informe. Para abrir una conexión con el explorador en el nodo raíz de la jerarquía de carpetas, solo tiene que especificar la dirección web del servidor de informes; a continuación, puede hacer clic en los vínculos de las carpetas para navegar por la jerarquía.  
  
 Al tener acceso a un directorio virtual de un servidor de informes, solo se visualizan las carpetas, los informes y los elementos cargados para los que se tiene permiso de acceso. La interfaz de usuario muestra únicamente la jerarquía de carpetas e información básica como, por ejemplo, la fecha de creación o modificación, el tamaño del archivo o el tipo de elemento de cada elemento:  
  
-   Un vínculo sin ningún otro indicador es un informe o un modelo.  
  
-   La etiqueta \<ds> indica un origen de datos compartido.  
  
-   La etiqueta \<dir> indica un elemento de carpeta.  
  
-   Una extensión de nombre de archivo indica que se trata de un recurso. La extensión del nombre del archivo identifica el tipo MIME del recurso. Por ejemplo, .jpg indica que se trata de una imagen en formato JPEG.  
  
## Escribir la dirección URL de un informe  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite el acceso con direcciones URL a determinados elementos de un servidor de informes. La dirección URL debe incluir una ruta de acceso completa al informe y comandos para representarlo. Si el informe incluye parámetros, también debe especificar cualquier valor necesario para abrir el informe. Si escribe una dirección URL para un informe que incluya espacios en la ruta de acceso, valores de parámetros o una extensión de representación, incluya en la dirección URL caracteres con codificación URL para obtener el resultado deseado. El siguiente ejemplo corresponde a una dirección URL de informe que incluye codificación para los espacios del nombre de la ruta de acceso, los parámetros y la extensión de representación:  
  
 `http://<Webservername>/reportserver?/<reportfolder>/employee+sales+summary&ReportYear=2004&ReportMonth=06&EmpID=24&rs:Command=Render&rs:Format=HTML4.0`  
  
 El límite máximo para una dirección URL en Internet Explorer es de 2.083 caracteres. Para obtener más información, vea [La longitud máxima de la dirección URL es de 2083 caracteres en Internet Explorer](http://support.microsoft.com/kb/208427).  
  
 Para obtener más información acerca de cómo obtener acceso a un informe a través de una URL, incluida la información acerca de cómo está construida una URL, vea el artículo sobre acceso a URL en la [documentación de Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) en los Libros en pantalla de SQL Server.  
  
  