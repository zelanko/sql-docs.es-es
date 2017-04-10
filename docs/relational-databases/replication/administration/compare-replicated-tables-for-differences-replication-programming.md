---
title: "Comparar tablas replicadas para buscar diferencias (programaci&#243;n de la replicaci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "tablediff, utilidad"
  - "comparar tablas replicadas"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Comparar tablas replicadas para buscar diferencias (programaci&#243;n de la replicaci&#243;n)
  Para determinar si los datos publicados en los artículos de tabla del publicador y el suscriptor no son idénticos, lo que puede indicar una falta de convergencia, se usa la validación de artículos. Para obtener más información, consulte [Validar datos replicados](../../../relational-databases/replication/validate-replicated-data.md). La validación, sin embargo, solo devuelve información sobre la existencia o no de diferencias, pero no indica las diferencias concretas entre las tablas de origen y destino. La utilidad de símbolo del sistema **tablediff** devuelve información detallada sobre las diferencias entre dos tablas y puede generar un script [!INCLUDE[tsql](../../../includes/tsql-md.md)] para establecer la convergencia de la suscripción con los datos del publicador.  
  
> [!NOTE]  
>  El **tablediff** utility sólo es compatible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servidores.  
  
### Para buscar diferencias en tablas replicarse con tablediff  
  
1.  En el símbolo del sistema de cualquier servidor incluido en una topología de replicación, ejecute la [tablediff Utility](../../../tools/tablediff-utility.md). Especifique los parámetros siguientes:  
  
    -   **-sourceserver** : el nombre del servidor en el que se conozcan los datos sea correcta, normalmente el publicador.  
  
    -   **-sourcedatabase** : el nombre de la base de datos que contiene los datos correctos.  
  
    -   **-sourcetable** : el nombre de la tabla de origen para el artículo que se va a comparar.  
  
    -   (Opcional) **-sourceschema** -propietario del esquema de la tabla de origen, si no el esquema predeterminado.  
  
    -   (Opcional) **-sourceuser** y **- sourcepassword** cuando se utiliza la autenticación de SQL Server para conectarse al publicador.  
  
        > [!IMPORTANT]  
        >  Siempre que sea posible, utilice la autenticación de Windows. Si debe usar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , pida a los usuarios que escriban las credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
    -   **-destinationserver** : el nombre del servidor en el que se está comparando los datos, normalmente un suscriptor.  
  
    -   **-destinationdatabase** : el nombre de una la base de datos que se están comparando.  
  
    -   **-destinationtable** : el nombre de la tabla que se va a comparar.  
  
    -   (Opcional) **-destinationschema** -propietario del esquema de la tabla de destino, si no el esquema predeterminado.  
  
    -   (Opcional) **-destinationuser** y **- destinationpassword** al usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticación para conectarse al suscriptor.  
  
        > [!IMPORTANT]  
        >  Siempre que sea posible, utilice la autenticación de Windows. Si debe usar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , pida a los usuarios que escriban las credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
    -   (Opcional) Use **- c** para realizar una comparación de nivel de columna.  
  
    -   (Opcional) Use **- q** para realizar un rápido, fila comparación recuento esquema única.  
  
    -   (Opcional) Especifique un nombre de archivo y ruta de acceso de **-o** a los resultados en un archivo.  
  
    -   (Opcional) Especificar una tabla de la base de datos de suscripción en la que se va a insertar los resultados de **-et**. Si la tabla ya existe, especifique **dt -** para quitar la tabla.  
  
    -   (Opcional) Use **-f** para generar un [!INCLUDE[tsql](../../../includes/tsql-md.md)] archivo corregir datos en el suscriptor para que coincidan con los datos en el publicador. Use **-df** para especificar el número de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones en cada archivo.  
  
    -   (Opcional) Use **-rc** y **-ri** para especificar el número de reintentos de una operación y el intervalo de reintento.  
  
    -   (Opcional) Use **-strict** para exigir la comparación estricta del esquema entre las tablas de origen y de destino.  
  
## Vea también  
 [Validar datos en el suscriptor](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  