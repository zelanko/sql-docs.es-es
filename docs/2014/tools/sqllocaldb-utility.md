---
title: SqlLocalDB (utilidad) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a3c83dfc8e7282ea67c3aff783ad4ec50826865
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330915"
---
# <a name="sqllocaldb-utility"></a>SqlLocalDB (utilidad)
  Use la `SqlLocalDB` utilidad para crear una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)] **LocalDB**. El `SqlLocalDB` utilidad (SqlLocalDB.exe) es una herramienta de línea de comandos simple que permite a los usuarios y desarrolladores crear y administrar una instancia de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB**. Para obtener información sobre cómo usar **LocalDB**, consulte [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name><instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] ["<user_SID>" | "<user_account>" ] "<private-name>""<shared-name>"  
    | [ unshare  | u ] "<shared-name>"  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* [**-s** ]  
 Crea una instancia de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. `SqlLocalDB` usa la versión de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] binarios especificados por * \<versión de la instancia >* argumento. El número de versión se especifica en formato numérico con al menos un decimal. Los números de versión secundaria (Service Pack) son opcionales. Como los siguientes dos números de versión son aceptables: 11.0 u 11.0.1186. La versión especificada se debe instalar en el equipo. Si no se especifica, el número de versión predeterminado es la versión de la `SqlLocalDB` utilidad. Al agregar **–s** se inicia la nueva instancia de **LocalDB**.  
  
 [ **share** | **h** ]  
 Comparte la instancia privada especificada de **LocalDB** por medio del nombre compartido especificado. Si se omite el SID del usuario o el nombre de la cuenta, usa de forma predeterminada el usuario actual.  
  
 [ **unshared** | **u** ]  
 Detiene el uso compartido de la instancia compartida especificada de **LocalDB**.  
  
 [ **delete** | **d** ] *\<instance-name>*  
 Elimina la instancia especificada de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**.  
  
 [ **start** | **s** ] "*\<instance-name>*"  
 Inicia la instancia especificada de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Cuando se realiza correctamente, la instrucción devuelve la dirección de la canalización con nombre de **LocalDB**.  
  
 [ **stop** | **p** ] *\<instance-name>* [**-i** ] [**-k** ]  
 Detiene la instancia especificada de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Agregar **– i** solicita el cierre de la instancia con el `NOWAIT` opción. Al agregar **–k** se elimina el proceso de la instancia sin ponerse en contacto con ella.  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 Muestra toda la instancia de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** que pertenece al usuario actual.  
  
 *\<instance-name>* devuelve el nombre, la versión, el estado (En ejecución o Detenido), la última hora de inicio de la instancia especificada de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** y el nombre de la canalización local de **LocalDB**.  
  
 [ **trace** | **t** ] **on** | **off**  
 **seguimiento en** habilita el seguimiento de la `SqlLocalDB` llamadas de API para el usuario actual. **trace off** deshabilita el seguimiento.  
  
 **-?**  
 Devuelve una descripción breve de cada uno de ellos `SqlLocalDB` opción.  
  
## <a name="remarks"></a>Notas  
 El argumento *instance name* debe cumplir las reglas de los identificadores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o debe incluirse entre comillas.  
  
 La ejecución de SqlLocalDB sin argumentos devuelve el texto de ayuda.  
  
 Las operaciones distintas de la operación de inicio solo se pueden realizar en una instancia perteneciente al usuario que ha iniciado la sesión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-an-instance-of-localdb"></a>A. Crear una instancia de LocalDB  
 En el ejemplo siguiente se crea una instancia de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** denominada `DEPARTMENT` utilizando los binarios de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y se inicia la instancia.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>B. Trabajar con una instancia compartida de LocalDB  
 Abra un símbolo del sistema utilizando los permisos de administrador.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd –S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 Ejecute el código siguiente para conectarse a la instancia compartida de **LocalDB** mediante el inicio de sesión de `NewLogin` .  
  
```  
sqlcmd –S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>Vea también  
 [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
  
