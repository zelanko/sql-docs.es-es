---
title: Crear archivos de valor de la Variable (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/17/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef98e5026d0cb488f0edfc4fccd386c0b1539bcd
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="creating-variable-value-files-accesstosql"></a>Crear archivos de valor de la Variable (AccessToSQL)
Un archivo de valores de Variable es un archivo XML que contiene los valores de parámetro de comandos (por ejemplo, el nombre de servidor de origen o destino) que cambian con frecuencia en migraciones de servidor. Cuando se produce un gran número de migraciones de base de datos, varios archivos de variable para almacenar el valor de cada servidor de origen se crean y se hace referencia en un archivo de script maestra con la **– v** cambiar en la línea de comandos. Este comportamiento ayuda a mantener los valores estáticos en unos pocos archivos de script con los valores de variables en varios archivos de variable.  
  
> [!NOTE]  
> -  Los nombres de variable son el prefijo y sufijo con un símbolo $ (dólar). Si una variable no se asigna un valor en el archivo de valor de la variable, producirá un error durante el análisis del archivo de script, da lugar a demora el proceso de ejecución de la consola.  
> -  The escape character for **$** is **$$**. Si el valor de un valor de variable o estático de un parámetro contiene un  **$**  símbolos (dólar), a continuación,  **$$**  debe especificarse para tratarlo como un carácter en lugar de una variable.  
> -  Por motivos de mantenimiento, las variables pueden declararse dentro de `‘variable-group’` elementos de una separación lógica de variables definidas por el usuario.  Uso de este elemento no es obligatorio.  
  
**Ejemplos:**  
  
**Ejemplo 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**Ejemplo 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Validación de valor de la variable de archivo  
El usuario puede validar fácilmente su archivo de valor de la variable en el archivo de definición de esquema **ConsoleScriptVariablesSchema.xsd** disponibles en la carpeta 'Esquemas'.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la utilización de la consola es [crear los archivos de conexión de servidor &#40; AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Crear los archivos de conexión de servidor (acceso)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
