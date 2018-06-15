---
title: Garantizar espacio suficiente en TempDB | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09db3f588a5631b02c3ce112dd1b10935537c311
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274134"
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantizar espacio suficiente en TempDB
Si se producen errores mientras se procesan [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que requieren espacio en Microsoft SQL Server 6.5 de procesamiento, deberá aumentar el tamaño de TempDB. (Algunas consultas requieren espacio de procesamiento temporal; por ejemplo, una consulta con una cláusula ORDER BY requiere un criterio de ordenación de la **Recordset**, lo que requiere espacio temporal.)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Lea este procedimiento antes de realizar las acciones porque no es tan fácil reducir un dispositivo una vez que se expande.  
  
> [!NOTE]
>  De forma predeterminada en Microsoft SQL Server 7.0 y versiones posterior, TempDB se establece para crecer automáticamente según sea necesario. Por lo tanto, este procedimiento solo puede ser necesario en servidores que ejecutan versiones anteriores a 7.0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Para aumentar el espacio de TempDB en SQL Server 6.5  
  
1.  Inicie el Administrador corporativo de Microsoft SQL Server, abra el árbol para el servidor y, a continuación, abra el árbol de dispositivos de la base de datos.  
  
2.  Seleccione un dispositivo (físico) para expandirlo, tal como Master y haga doble clic en el dispositivo para abrir el **Editar dispositivo de base de datos** cuadro de diálogo.  
  
     Este cuadro de diálogo muestra cuánto espacio están utilizando las bases de datos actuales.  
  
3.  En el **tamaño** cuadro, aumente el dispositivo a la cantidad deseada (por ejemplo, 50 megabytes (MB) de espacio en disco duro).  
  
4.  Haga clic en **cambiar ahora** para aumentar la cantidad de espacio en el que se puede expandir TempDB (lógica).  
  
5.  Abra el árbol de las bases de datos en el servidor y, a continuación, haga doble clic en **TempDB** para abrir el **Editar base de datos** cuadro de diálogo. El **base de datos** pestaña muestra la cantidad de espacio asignado a TempDB (**tamaño de los datos**). De forma predeterminada, esto es 2 MB.  
  
6.  En el **tamaño** grupo, haga clic en **expandir**. Los gráficos muestran el espacio disponible y utilizado en cada uno de los dispositivos físicos. Las barras en color granate representan espacio disponible.  
  
7.  Seleccione un **dispositivo de registro**, tal como patrón, para mostrar el tamaño disponible en el **tamaño (MB)** cuadro.  
  
8.  Haga clic en **expandir ahora** para asignar ese espacio a la base de datos TempDB.  
  
     El **Editar base de datos** cuadro de diálogo muestra el nuevo tamaño asignado para TempDB.  
  
 Para obtener más información acerca de este tema, busque el archivo de Ayuda de Microsoft SQL Server Enterprise Manager de "Cuadro de diálogo base de datos de expansión".  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


