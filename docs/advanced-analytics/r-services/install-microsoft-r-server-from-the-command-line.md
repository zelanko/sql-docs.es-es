---
title: "Instalar Microsoft R Server desde la l&#237;nea de comandos | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# Instalar Microsoft R Server desde la l&#237;nea de comandos
    
Puede instalar Microsoft R Server desde la línea de comandos usando las funciones de scripting proporcionadas con la instalación de SQL Server. 

- Para efectuar una instalación **desatendida**, debe especificar la ubicación de la utilidad de instalación y usar argumentos para indicar las características que quiere instalar. 
- Para efectuar una instalación **silenciosa**, proporcione los mismos argumentos y agregue el conmutador **/q**. No se proporcionará ningún mensaje y no se requiere ninguna interacción, pero se producirá un error en el programa de instalación si se omite alguno de los argumentos obligatorios.

Para obtener más información, vea [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="perform-a-command-line-install-of-microsoft-r-server-standalone"></a>Efectuar una instalación de línea de comandos de Microsoft R Server (independiente)

 En los ejemplos siguientes se muestran los argumentos usados al efectuar una instalación de línea de comandos de Microsoft R Server mediante el programa de instalación de SQL Server.


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>Ejemplo de instalación desatendida de Microsoft R Server independiente

Ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados para instalar solo Microsoft R Server (independiente) y sus requisitos previos. 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

Para consultar el progreso y ver los mensajes, quite el argumento/q.

Tenga en cuenta que los argumentos siguientes son obligatorios:
  - **FEATURES = SQL_SHARED_MR** obtiene únicamente los componentes de Microsoft R Server, incluidos Microsoft R Open y los requisitos previos.
  - **IACCEPTROPENLICENSETERMS** indica que ha aceptado los términos de la licencia para usar los componentes de R de código abierto.
  - **IACCEPTSQLSERVERLICENSETERMS** es obligatorio para ejecutar el Asistente para la instalación.


### <a name="offline-installation"></a>Instalación sin conexión

Si instala Microsoft R Server (independiente) en un equipo que no tiene acceso a Internet, debe descargar primero los componentes de R necesarios y copiarlos en una carpeta local. Para consultar las ubicaciones de descarga, consulte [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   


## <a name="advanced-installation-tips"></a>Sugerencias de instalación avanzada

Una vez concluida la instalación, puede revisar el archivo de configuración creado por el programa de instalación de SQL Server, junto con un resumen de las acciones de instalación.

De forma predeterminada, todos los registros de y resúmenes de instalación de SQL Server, así como las características relacionadas, se crean en `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`.

Se crea una subcarpeta independiente para cada característica instalada. En el caso de Microsoft R Server, busque lo siguiente: 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

Para configurar otra instancia de Microsoft R Server con los mismos parámetros, puede reutilizar el archivo de configuración que se crea durante la instalación. Para obtener más información, consulte [Instalar SQL Server mediante un archivo de configuración](https://msdn.microsoft.com/library/dd239405.aspx).



### <a name="customizing-your-r-environment"></a>Personalizar el entorno de R

Después de la instalación, puede instalar más paquetes de R. Para obtener más información, consulte [Installing and Managing R Packages](../../advanced-analytics/r-services/installing-and-managing-r-packages.md) (Instalar y administrar paquetes de R).

> [!IMPORTANT]
> Si va a ejecutar el código de R en SQL Server, asegúrese de instalar los mismos paquetes en el equipo cliente que ejecuta Microsoft R Server y en la instancia de SQL Server que ejecuta Servicios de R. 



## <a name="see-also"></a>Vea también  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  