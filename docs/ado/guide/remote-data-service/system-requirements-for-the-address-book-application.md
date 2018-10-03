---
title: Requisitos del sistema para la dirección de reservar la aplicación | Microsoft Docs
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
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9af5257d5714e391d31415758d1b4ab66d7b9da2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636023"
---
# <a name="system-requirements-for-the-address-book-application"></a>Requisitos del sistema para la aplicación de la libreta de direcciones
Para configurar la aplicación de ejemplo de la libreta de direcciones, es preciso cumplir los requisitos de software y la base de datos siguientes:  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Los requisitos de software del equipo de servidor para ejecutar esta aplicación Web se incluyen:  
  
-   Microsoft Windows NT® Server 4.0 con Service Pack 3 o posterior, o Microsoft Windows® 2000 Server.  
  
-   Microsoft Internet Information Services (IIS) versión 3.0 o posterior, con las páginas Active Server.  
  
 Los requisitos de software del equipo cliente para ejecutar esta aplicación Web se incluyen:  
  
-   Microsoft Internet Explorer 4.0 o posterior.  
  
-   Estación de trabajo de Microsoft Windows NT 4.0 o Server, Windows 2000 o Microsoft Windows 98.  
  
## <a name="database-requirements"></a>Requisitos de base de datos  
 Para usar este ejemplo, debe tener:  
  
-   Servidor de base de datos de un operativos Microsoft® SQL Server versión 6.5 o versiones posterior.  
  
-   Privilegios para crear la base de datos y rellenarlo con los datos de ejemplo.  
  
-   Comprobación de los datos mediante el Administrador corporativo o las utilidades ISQL (denominado analizador de consultas en SQL Server 7.0).  
  
 Si no tiene privilegios, el Administrador de base de datos posible que deba configurar el sistema y concederle permisos de acceso a la base de datos, o configurar la base de datos para usted.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar el Script SQL de libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Ejecución de la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


