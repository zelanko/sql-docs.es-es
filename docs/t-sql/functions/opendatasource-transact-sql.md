---
title: OPENDATASOURCE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd106322dfc78186aefaadac42622852d87d40f2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información de conexión ad hoc como parte de un nombre de objeto de cuatro partes sin utilizar un nombre de servidor vinculado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>Argumentos  
 *NombreProveedor*  
 Es el nombre registrado como PROGID del proveedor OLE DB utilizado para obtener acceso al origen de datos. *NombreProveedor* es un **char** tipo de datos, sin valor predeterminado.  
  
 *init_string*  
 Es la cadena de conexión que se pasa a la interfaz IDataInitialize del proveedor de destino. La sintaxis de cadena de proveedor se basa en pares de palabra clave y valor separados por punto y coma, por ejemplo: **'***palabraclave1*=*valor***;** *palabraclave2*=*valor***'**.  
  
 Para conocer los pares de palabra clave y valor admitidos, vea [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK. En esta documentación se define la sintaxis básica. La siguiente tabla se palabras clave de las listas utilizadas con más frecuencia en el *init_string* argumento.  
  
|Palabra clave|Propiedad OLE DB|Valores válidos y descripción|  
|-------------|---------------------|----------------------------------|  
|Origen de datos|DBPROP_INIT_DATASOURCE|Nombre del origen de datos al que se va a conectar. Distintos proveedores lo interpretan de formas distintas. Para un proveedor OLE DB de SQL Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , indica el nombre del servidor. Para un proveedor OLE DB para Jet, indica la ruta de acceso completa al archivo .mdb o al archivo .xls.|  
|Ubicación|DBPROP_INIT_LOCATION|Ubicación de la base de datos a la que se va a conectar.|  
|Propiedades extendidas|DBPROP_INIT_PROVIDERSTRING|Cadena de conexión específica del proveedor.|  
|Tiempo de espera de conexión|DBPROP_INIT_TIMEOUT|Valor de tiempo de espera después del cual se produce un error en el intento de conexión.|  
|Id. de usuario|DBPROP_AUTH_USERID|Id. de usuario que se va a utilizar para la conexión.|  
|Contraseña|DBPROP_AUTH_PASSWORD|Contraseña que se va a utilizar para la conexión.|  
|Catálogo|DBPROP_INIT_CATALOG|Nombre del catálogo inicial o predeterminado al conectarse al origen de datos.|  
|Seguridad integrada|DBPROP_AUTH_INTEGRATED|SSPI, para especificar la autenticación de Windows|  
  
## <a name="remarks"></a>Comentarios  
 OPENDATASOURCE se puede utilizar para tener acceso a datos remotos desde orígenes de datos de OLE DB solo cuando la opción de Registro DisallowAdhocAccess está establecida explícitamente en 0 para el proveedor especificado y la opción de configuración avanzada Ad Hoc Distributed Queries está habilitada. Cuando no se establecen estas opciones, el comportamiento predeterminado no permite el acceso ad hoc.  
  
 Es posible utilizar la función OPENDATASOURCE en las mismas ubicaciones de la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] de un nombre del servidor vinculado. Por tanto, se puede utilizar OPENDATASOURCE como la primera parte de un nombre de cuatro partes que hace referencia a un nombre de tabla o vista en una instrucción SELECT, INSERT, UPDATE o DELETE, o a un procedimiento almacenado remoto en una instrucción EXECUTE. Cuando se ejecutan procedimientos almacenados remotos, OPENDATASOURCE debe hacer referencia a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. OPENDATASOURCE no acepta variables como argumentos.  
  
 Al igual que la función OPENROWSET, OPENDATASOURCE solo debe hacer referencia a orígenes de datos OLE DB a los que se tiene acceso con poca frecuencia. Defina un servidor vinculado para los orígenes de datos a los que tiene acceso varias veces. Ni OPENDATASOURCE ni OPENROWSET proporcionan toda la funcionalidad de definiciones de servidores vinculados, como la administración de seguridad y la capacidad de consultar información de catálogos. Toda la información de conexión, incluidas las contraseñas, se debe proporcionar siempre que se llama OPENDATASOURCE.  
  
> [!IMPORTANT]  
>  La autenticación de Windows es mucho más segura que la de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Siempre que sea posible, debe utilizar la Autenticación de Windows. OPENDATASOURCE no se debe utilizar con contraseñas explícitas en la cadena de conexión.  
  
 Los requisitos de conexión de cada proveedor son similares a los requisitos de esos parámetros cuando se crean servidores vinculados. Los detalles de muchos proveedores comunes se enumeran en el tema [sp_addlinkedserver &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 Las llamadas a OPENDATASOURCE, OPENQUERY u OPENROWSET en la cláusula FROM se evalúan por separado y de forma independiente de otras llamadas a estas funciones utilizadas como destino de la actualización, incluso si se han suministrado argumentos idénticos a las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
## <a name="permissions"></a>Permissions  
 Todos los usuarios pueden ejecutar OPENDATASOURCE. Los permisos que se utilizan para conectarse al servidor remoto se determinan a partir de la cadena de conexión.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una conexión ad hoc a la instancia de `Payroll` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor `London`, y se consulta la tabla `AdventureWorks2012.HumanResources.Employee`. (El uso de SQLNCLI y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redirigirá a la última versión del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client).  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 En el ejemplo siguiente se crea una conexión ad hoc a una hoja de cálculo de Excel en el formato 1997 - 2003.  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>Vea también  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  

