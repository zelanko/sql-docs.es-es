---
title: Escenario RDS | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 920df727d2714629a45280133c53011afccc5c4d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="rds-scenario"></a>Escenario RDS
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La aplicación de la libreta de direcciones es un escenario que muestra cómo utilizar el servicio de datos remoto (RDS) para compilar una aplicación Web simple y orientadas a datos, una libreta de direcciones de la empresa en línea. Este escenario es útil para Microsoft Visual Basic Scripting Edition (VBScript) y los programadores de COM que desean aprender a usar los controles ActiveX compatibles con datos con RDS y software con más experiencia de los desarrolladores que desean crear aplicaciones Web basadas en datos.  
  
 Este escenario se supone que sabe cómo usar etiquetas de diseño básico HTML, técnicas de enlace de datos de uso DHTML y programa con controles ActiveX.  
  
 Si ha instalado el SDK, el código fuente completo para la aplicación de ejemplo de libreta de direcciones puede encontrarse en el directorio del SDK en samples\dataaccess\rds\AddressBook\AddressBook.asp. Para ver el escenario de libreta de direcciones, escriba en Internet Explorer 4.0 o posterior,  **http://*webserver*/RDS/AddressBook/AddressBook.asp** donde *webserver* es el nombre Dado que el equipo de servidor de Windows NT 4.0 o Windows 2000 Web que ejecuta Internet Information Services (IIS) y ASP.  
  
## <a name="introduction-to-address-book"></a>Introducción a la libreta de direcciones  
 La aplicación de ejemplo de libreta de direcciones proporciona una libreta de direcciones de en línea simple que puede usar para publicar un directorio de búsqueda a través de una intranet. La libreta de direcciones está diseñada para que un usuario puede escribir una cadena de búsqueda en uno o varios campos para solicitar información acerca de los empleados. Para mostrar las características básicas del servicio de datos remoto, la aplicación de ejemplo se mantiene intencionadamente poco a poco, con un número mínimo de objetos y los campos de búsqueda.  
  
 La interfaz de la aplicación consta de las siguientes partes:  
  
-   Un elemento que no son de visual **RDS. DataControl** objeto de enlace de datos que se usa el cliente para conectarse a la base de datos.  
  
-   Criterios de búsqueda de los cuadros de texto HTML que actúan como campos de entrada para el atributo de empleado.  
  
-   Botones de comando HTML para generar consultas, borrar campos de búsqueda, actualizar la base de datos con la información de empleado, cancelar los cambios pendientes y navegar por las filas de datos que se muestran en la cuadrícula.  
  
-   DHTML enlace de datos para mostrar los datos devueltos por las consultas realizadas en una base de datos back-end (a través de la **RDS. DataControl** objeto de enlace de datos) en una tabla.  
  
-   Rutinas de VBScript que se conectan a cada uno de los elementos que se mencionaron anteriormente y que puedan interactuar. También se utiliza código VBScript para inicializar el **RDS. DataControl** de objetos y crear dinámicamente los encabezados de columna en la tabla HTML de los nombres de los **RDS. DataControl** campos de conjunto de registros.  
  
 Siga los vínculos de paso a paso para configurar y ejecutar el escenario y para obtener más información sobre cómo funciona el escenario.  
  
 Este escenario contiene los temas siguientes.  
  
-   [Requisitos del sistema para la aplicación de la libreta de direcciones](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Ejecutar el Script SQL de libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Ejecuta la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Objeto de enlace de datos de libreta de direcciones](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Botones de comando de libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Botones de navegación de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos del sistema para la aplicación de la libreta de direcciones](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Conceptos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)



