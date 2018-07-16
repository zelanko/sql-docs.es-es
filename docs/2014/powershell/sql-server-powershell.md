---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f605305a86295f8b2e91aa7300086c5827e683d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271141"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] admite Windows PowerShell, que es un poderoso shell de scripting que permite a los administradores y desarrolladores automatizar la administración de servidores y la implementación de aplicaciones. El lenguaje de Windows PowerShell admite una lógica más compleja que los scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] , con lo que se permite a los administradores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] generar poderosos scripts de administración. Los scripts de Windows PowerShell también se pueden utilizar para administrar otros productos de servidor de [!INCLUDE[msCoName](../includes/msconame-md.md)] . Esto ofrece a los administradores un lenguaje común de scripting para los diferentes servidores.  
  
## <a name="sql-server-powershell-components"></a>Componentes de SQL Server PowerShell  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona un módulo de Windows PowerShell denominado `sqlps` que se usa para importar componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un entorno o un script de Windows PowerShell 2.0. Las cargas de módulo `sqlps`, dos complementos de Windows PowerShell que implementan:  
  
-   Un proveedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , que habilita un mecanismo de navegación sencillo similar a las rutas de acceso al sistema de archivos. Puede compilar rutas de acceso similares a las del sistema de archivos, en las que la unidad se asocia a un modelo de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los nodos se basan en las clases del modelo de objetos. A continuación, puede usar comandos conocidos, como **cd** y **dir** , para navegar por las rutas de acceso de modo similar a como se navega por las carpetas en una ventana del símbolo del sistema. Puede usar otros comandos, como **ren** o **del**, para realizar acciones en los nodos de la ruta de acceso.  
  
-   Un conjunto de cmdlets, que son comandos que se usan en los scripts de Windows PowerShell para especificar una acción de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Las cargas de módulo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admiten acciones tales como la ejecución de un script de **sqlcmd** que contenga instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] o de consultas.  
  
 Para obtener información acerca de Windows PowerShell, vea la [Guía de Introducción de Windows PowerShell](http://msdn.microsoft.com/library/hh857337.aspx).  
  
## <a name="sql-server-versions"></a>versiones de SQL Server  
 Los componentes de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell pueden usarse para administrar instancias de [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] o versiones posteriores. Las instancias de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] deben ejecutar SP2 o posterior. Las instancias de [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] deben ejecutar SP4 o posterior. Cuando se usan componentes de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell con versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se limitan a la funcionalidad disponible en esas versiones.  
  
## <a name="sql-server-powershell-tasks"></a>Tareas de SQL Server PowerShell  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe el mecanismo preferido para ejecutar el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] componentes de PowerShell; para abrir una sesión de PowerShell y cargar el `sqlps` módulo. Las cargas de módulos `sqlps` de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] del proveedor y cmdlets de PowerShell, y los ensamblados (SMO) de objetos de administración de SQL Server usados por el proveedor y cmdlets.|[Importar el módulo SQLPS](../database-engine/import-the-sqlps-module.md)|  
|Describe cómo cargar solo los ensamblados SMO sin el proveedor o los cmdlets.|[Cargar ensamblados SMO en Windows PowerShell](load-the-smo-assemblies-in-windows-powershell.md)|  
|Describe cómo ejecutar una sesión de Windows PowerShell haciendo clic con el botón derecho en un nodo del **Explorador de objetos**. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] inicia una sesión de Windows PowerShell, carga el `sqlps` módulo y establece la ruta de acceso del proveedor de SQL Server en el objeto seleccionado.|[Ejecutar Windows PowerShell desde SQL Server Management Studio](run-windows-powershell-from-sql-server-management-studio.md)|  
|Describe cómo crear los pasos de trabajo del Agente SQL Server que ejecutan un script de Windows PowerShell. Los trabajos entonces se pueden programar para ejecutarse a horas específicas o en respuesta a eventos.|[Pasos de ejecución de Windows PowerShell del Agente SQL Server] (run-windows-powershell-steps-in-sql-server-agent.md
)|  
|Describe cómo usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por una jerarquía de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|[Proveedor de SQL Server PowerShell Provider](sql-server-powershell-provider.md)|  
|Describe cómo usar los cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que especifican acciones de [!INCLUDE[ssDE](../includes/ssde-md.md)] como ejecutar un script de [!INCLUDE[tsql](../includes/tsql-md.md)] .|[Usar los cmdlets del motor de base de datos](../database-engine/use-the-database-engine-cmdlets.md)|  
|Describe cómo especificar los identificadores delimitados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contienen caracteres no admitidos por Windows PowerShell.|[Identificadores de SQL Server en PowerShell](sql-server-identifiers-in-powershell.md)|  
|Describe cómo realizar conexiones con la autenticación de SQL Server. De forma predeterminada, los componentes de PowerShell de SQL Server usan conexiones con autenticación de Windows mediante las credenciales del proceso que ejecuta Windows PowerShell.|[Administrar la autenticación en PowerShell del motor de base de datos](manage-authentication-in-database-engine-powershell.md)|  
|Describe cómo usar las variables que implementa el proveedor de PowerShell de SQL Server para controlar cuántos objetos se muestran al usar la finalización mediante el tabulador de Windows PowerShell. Esto es especialmente útil cuando se trabaja en las bases de datos que contienen una gran cantidad de objetos.|[Administrar la finalización mediante tabulador &#40;SQL Server PowerShell&#41;](manage-tab-completion-sql-server-powershell.md)|  
|Describe cómo usar Get-Help para obtener información acerca de los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el entorno de Windows PowerShell.|[Get Help SQL Server PowerShell](../database-engine/get-help-sql-server-powershell.md)|  
  
  
