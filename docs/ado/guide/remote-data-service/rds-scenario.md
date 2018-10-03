---
title: Escenario RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aaeedb6dffb992ac940eebd450c63d33badb299d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845283"
---
# <a name="rds-scenario"></a>Escenario de RDS
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La aplicación Libreta de direcciones es un escenario que se muestra cómo usar el servicio de datos remoto (RDS) para compilar una aplicación Web simple, basada en datos, una libreta de direcciones de la empresa en línea. Este escenario es útil para Microsoft Visual Basic Scripting Edition (VBScript) y los programadores de COM que desean aprender a usar controles ActiveX compatibles con datos con RDS y software con más experiencia de los desarrolladores que desean crear aplicaciones Web centradas en datos.  
  
 Este escenario se supone que sabe cómo usar las etiquetas de diseño básico HTML, técnicas de enlace de datos de uso DHTML y programa con controles ActiveX.  
  
 Si ha instalado el SDK, el código fuente completo para la aplicación de ejemplo de la libreta de direcciones puede encontrarse en el directorio SDK en samples\dataaccess\rds\AddressBook\AddressBook.asp. Para ver el escenario de libreta de direcciones, escriba en Internet Explorer 4.0 o posterior, **http://*webserver*/RDS/AddressBook/AddressBook.asp** donde *webserver* es el nombre dado en el equipo de servidor de Windows NT 4.0 o Windows 2000 Web se está ejecutando Internet Information Services (IIS) y ASP.  
  
## <a name="introduction-to-address-book"></a>Introducción a la libreta de direcciones  
 La aplicación de ejemplo de la libreta de direcciones proporciona una libreta de direcciones de en línea simple que puede usar para publicar un directorio que se puede buscar en una intranet. La libreta de direcciones está diseñada para que un usuario puede escribir una cadena de búsqueda en uno o varios campos para solicitar información acerca de los empleados. Para mostrar las características básicas de servicio de datos remoto, la aplicación de ejemplo se mantiene deliberadamente pequeña, con un número mínimo de objetos y campos de búsqueda.  
  
 La interfaz de la aplicación consta de las siguientes partes:  
  
-   Un objeto no visual **RDS. DataControl** objeto de enlace de datos que se usa el cliente para conectarse a la base de datos.  
  
-   Criterios de búsqueda de los cuadros de texto HTML que actúan como campos de entrada para el atributo de empleado.  
  
-   Botones de comando HTML para generar consultas, borrar campos de búsqueda, actualice la base de datos con información de los empleados, cancelar los cambios pendientes y navegar por las filas de datos que se muestran en la cuadrícula.  
  
-   DHTML enlace de datos para mostrar los datos devueltos por las consultas en una base de datos back-end (a través de la **RDS. DataControl** objeto de enlace de datos) en una tabla.  
  
-   Rutinas de VBScript que se conectan cada uno de los elementos que se mencionaron anteriormente y que puedan interactuar. Código de VBScript también se usa para inicializar el **RDS. DataControl** de objetos y crear dinámicamente los encabezados de columna en la tabla HTML de los nombres de los **RDS. DataControl** campos de conjunto de registros.  
  
 Siga los vínculos de paso a paso para configurar y ejecutar el escenario y para obtener más información sobre cómo funciona el escenario.  
  
 Este escenario contiene los temas siguientes.  
  
-   [Requisitos del sistema para la aplicación de la libreta de direcciones](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Ejecución del script de SQL de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Ejecución de la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Objeto de enlace de datos de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Botones de navegación de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos del sistema para la aplicación de la libreta de direcciones](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Conceptos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)


