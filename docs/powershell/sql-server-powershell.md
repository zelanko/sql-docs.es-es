---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.prod_service: powershell
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c8736ee258f072685bd7919b98c15a5704873fbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[Instalación de SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: **SqlServer** y **SQLPS**. El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**. El módulo **SqlServer** contiene versiones actualizadas de los cmdlets en **SQLPS**, así como nuevos cmdlets para admitir las características más recientes de SQL.  
> Las versiones anteriores del módulo **SqlServer** *estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la Galería de PowerShell.
> Para instalar el módulo **SqlServer**, consulte [Instalar SQL Server PowerShell](download-sql-server-ps-module.md).

**¿Por qué ha cambiado el módulo de SQLPS a SqlServer?**

Para enviar las actualizaciones de SQL PowerShell era necesario cambiar la identidad del módulo de SQL PowerShell, así como el contenedor conocido como *SQLPS.exe*. Debido a este cambio, ahora hay dos módulos de SQL PowerShell, **SqlServer** y **SQLPS**.  

**Actualice los scripts de PowerShell si importan el módulo SQLPS.**

Si tiene algún script de PowerShell que ejecute `Import-Module -Name SQLPS` y quiere aprovechar la nueva funcionalidad de proveedor y los nuevos cmdlets, debe cambiarlos a `Import-Module -Name SqlServer`. El módulo nuevo se instala en la carpeta `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer`. Por tanto, no tiene que actualizar la variable $env:PSModulePath. Si tiene scripts que usan una versión comunitaria o de terceros de un módulo denominado **SqlServer**, use el parámetro Prefix para evitar conflictos de nombres. No hay ningún cambio en el módulo que usa el Agente SQL Server. 

  
## <a name="sql-server-powershell-components"></a>Componentes de SQL Server PowerShell  
El módulo **SqlServer** carga dos complementos de Windows PowerShell:  
  
-   Un proveedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , que habilita un mecanismo de navegación sencillo similar a las rutas de acceso al sistema de archivos. Puede compilar rutas de acceso similares a las del sistema de archivos, en las que la unidad se asocia a un modelo de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los nodos se basan en las clases del modelo de objetos. A continuación, puede usar comandos conocidos, como **cd** y **dir** , para navegar por las rutas de acceso de modo similar a como se navega por las carpetas en una ventana del símbolo del sistema. Puede usar otros comandos, como **ren** o **del**, para realizar acciones en los nodos de la ruta de acceso.  
  
-   Un conjunto de cmdlets que admiten acciones tales como la ejecución de un script de **sqlcmd** que contenga instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] o de XQuery.  
  
  
## <a name="sql-server-versions"></a>versiones de SQL Server  
Los cmdlets de SQL PowerShell se pueden usar para administrar instancias de Azure SQL Database, Azure SQL Data Warehouse y todos los [productos de SQL Server compatibles](https://support.microsoft.com/lifecycle/search/1044).  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>Identificadores de SQL Server que contienen caracteres no admitidos en las rutas de acceso de PowerShell  
 
Los cmdlets **Encode-Sqlname** y **Decode-Sqlname** le ayudan a especificar los identificadores de SQL Server que contienen caracteres no admitidos en las rutas de acceso de PowerShell. Para más información, consulte [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md).  
  
Use el cmdlet **Convert-UrnToPath** para convertir un nombre de recurso único de un objeto de [!INCLUDE[ssDE](../includes/ssde-md.md)] en una ruta de acceso para el proveedor de SQL Server PowerShell. Para más información, consulte [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Expresiones de consulta y nombres de recursos únicos  

Las expresiones de consulta son cadenas que usan una sintaxis similar a XPath para especificar un conjunto de criterios que enumeran uno o más objetos de una jerarquía del modelo de objetos. Un nombre de recurso único (URN) es un tipo específico de cadena de expresión de consulta que identifica exclusivamente un objeto único. Para más información, consulte [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md).       


## <a name="cmdlet-reference"></a>Referencia de cmdlets
* [Cmdlets de SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets de SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
