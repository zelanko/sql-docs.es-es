---
title: Conectar con una base de datos de origen de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e82b9d2621b034b9b5a6d19aaec856ab6ec81a48
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438782"
---
# <a name="connect-to-an-oracle-source-database"></a>Conectar con una base de datos de origen de Oracle
  Use la página Oracle Source para proporcionar la información necesaria para conectarse a la base de datos de origen de Oracle. La instancia CDC leerá los registros Rehacer de la base de datos de Oracle a la que está conectado.  
  
 **Cadena de conexión de Oracle**  
 Escriba la cadena de conexión de Oracle al equipo que tiene la base de datos de Oracle que está usando. La cadena de conexión se escribe de una de las maneras siguientes:  
  
 `host[:port][/service name]`  
  
 La cadena de conexión también puede especificar un descriptor de conexión de Oracle Net, por ejemplo `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 Si se usa un servidor de directorio o tnsnames, la cadena de conexión puede ser el nombre de la conexión.  
  
 **Autenticación de minería de registros de Oracle**  
 Para especificar las credenciales del usuario de la base de datos de Oracle que tiene autorización para realizar minería de registros, seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**: seleccione esta opción para usar las credenciales del dominio de Windows actual. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: si selecciona esta opción, debe escribir el **Nombre de usuario** y la **Contraseña** para el usuario en la base de datos de Oracle a la que se está conectando.  
  
> [!NOTE]
>  Un usuario debe tener concedidos los privilegios siguientes en la base de datos de Oracle para poder ser un usuario de minería de registros.  
> 
>  -   SELECCIONAR activado\<any-captured-table>  
> -   SELECT ANY TRANSACTION  
> -   EXECUTE en DBMS LOGMNR  
> -   SELECT en V$LOGMNR CONTENTS  
> -   SELECT en V$ARCHIVED LOG  
> -   SELECT en V$LOG  
> -   SELECT en V$LOGFILE  
> -   SELECT en V$DATABASE  
> -   SELECT en V$THREAD  
> -   SELECT en ALL INDEXES  
> -   SELECT en ALL OBJECTS  
> -   SELECT en DBA OBJECTS  
> -   SELECT en ALL TABLES  
> 
>  Si alguno de estos privilegios no se puede conceder a un V$xxx, concédalo al V_S$xxx.  
  
 **Probar conexión**  
 Haga clic en **Probar conexión** para determinar si se estableció una conexión con el equipo remoto que tiene la base de datos de Oracle. Aparecerá un cuadro de diálogo para informarle si la conexión se realizó correctamente.  
  
> [!IMPORTANT]  
>  Debido a un problema conocido, se puede producir un error en la conexión con la base de datos de origen de Oracle si el Diseñador CDC no se ejecuta como administrador. Si se produce un error en la conexión, cierre y reinicie el Diseñador CDC usando la opción **Ejecutar como administrador** .  
  
 Cuando termine de especificar información en esta página, haga clic en **Siguiente** para [Select Oracle Tables and Columns](select-oracle-tables-and-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Editar propiedades de la instancia](edit-instance-properties.md)  
  
  
