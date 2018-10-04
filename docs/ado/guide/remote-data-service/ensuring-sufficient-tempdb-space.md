---
title: Garantizar espacio suficiente de TempDB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc4fd9d29c7623b3c814f0e45904e55463defe0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666583"
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantía de espacio suficiente de TempDB
Si se producen errores al control [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) los objetos que requieren espacio en Microsoft SQL Server 6.5 de procesamiento, es posible que deba aumentar el tamaño de TempDB. (Algunas consultas requieren espacio temporal de procesamiento; por ejemplo, una consulta con una cláusula ORDER BY requiere un criterio de ordenación de la **Recordset**, lo que requiere algo de espacio temporal.)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Lea este procedimiento antes de realizar las acciones porque no es tan fácil reducir un dispositivo una vez que se expande.  
  
> [!NOTE]
>  De forma predeterminada en Microsoft SQL Server 7.0 y versiones posterior, TempDB se establece para crecer automáticamente según sea necesario. Por lo tanto, este procedimiento solo puede ser necesaria en servidores que ejecutan versiones anteriores a 7.0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Para aumentar el espacio de TempDB en SQL Server 6.5  
  
1.  Iniciar el Administrador corporativo de Microsoft SQL Server, abra el árbol para el servidor y, a continuación, abra el árbol de los dispositivos de la base de datos.  
  
2.  Seleccione un dispositivo (físico) para expandir, tal como patrón y haga doble clic en el dispositivo para abrir el **Editar dispositivo de base de datos** cuadro de diálogo.  
  
     Este cuadro de diálogo muestra cuánto espacio están utilizando las bases de datos actuales.  
  
3.  En el **tamaño** cuadro, aumente el dispositivo a la cantidad deseada (por ejemplo, 50 megabytes (MB) de espacio en disco).  
  
4.  Haga clic en **cambiar ahora** para aumentar la cantidad de espacio a la que se puede expandir TempDB (lógico).  
  
5.  Abrir el árbol de las bases de datos en el servidor y, a continuación, haga doble clic en **TempDB** para abrir el **Editar base de datos** cuadro de diálogo. El **base de datos** pestaña muestra la cantidad de espacio asignado actualmente a TempDB (**tamaño de los datos**). De forma predeterminada, esto es 2 MB.  
  
6.  En el **tamaño** grupo, haga clic en **expandir**. Los gráficos muestran el espacio disponible y asignado en cada uno de los dispositivos físicos. Las barras de color granate representan espacio disponible.  
  
7.  Seleccione un **dispositivo de registro**, tal como patrón, para mostrar el tamaño disponible en el **tamaño (MB)** cuadro.  
  
8.  Haga clic en **expandir ahora** para asignar ese espacio a la base de datos TempDB.  
  
     El **Editar base de datos** cuadro de diálogo muestra el nuevo tamaño asignado para TempDB.  
  
 Para obtener más información acerca de este tema, busque el archivo de Ayuda de Microsoft SQL Server Enterprise Manager para "Cuadro de diálogo base de datos de expansión".  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


