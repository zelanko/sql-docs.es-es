---
title: OPENDATASOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d0584e0dd56cdeb58e525478f88fa9bed142e223
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914789"
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Proporciona información de conexión ad hoc como parte de un nombre de objeto de cuatro partes sin utilizar un nombre de servidor vinculado.  

 ![Icono de vínculo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 Es el nombre registrado como PROGID del proveedor OLE DB utilizado para obtener acceso al origen de datos. *provider_name* es un tipo de datos **char** que carece de valor predeterminado.  
  
 *init_string*  
 Es la cadena de conexión que se pasa a la interfaz IDataInitialize del proveedor de destino. La sintaxis de cadena del proveedor se basa en pares de palabra clave y valor separados por puntos y coma, como: **"** _palabra clave 1_=_valor_ **;** _palabra clave 2_=_valor_ **"** .  
  
 Para conocer los pares de palabra clave y valor admitidos, vea [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK. En esta documentación se define la sintaxis básica. En la siguiente tabla se muestran las palabras clave más utilizadas en el argumento *init_string*.  
  
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
  
## <a name="remarks"></a>Notas  
 OPENDATASOURCE se puede utilizar para tener acceso a datos remotos desde orígenes de datos de OLE DB solo cuando la opción de Registro DisallowAdhocAccess está establecida explícitamente en 0 para el proveedor especificado y la opción de configuración avanzada Ad Hoc Distributed Queries está habilitada. Cuando no se establecen estas opciones, el comportamiento predeterminado no permite el acceso ad hoc.  
  
 Es posible utilizar la función OPENDATASOURCE en las mismas ubicaciones de la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] de un nombre del servidor vinculado. Por tanto, se puede utilizar OPENDATASOURCE como la primera parte de un nombre de cuatro partes que hace referencia a un nombre de tabla o vista en una instrucción SELECT, INSERT, UPDATE o DELETE, o a un procedimiento almacenado remoto en una instrucción EXECUTE. Cuando se ejecutan procedimientos almacenados remotos, OPENDATASOURCE debe hacer referencia a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. OPENDATASOURCE no acepta variables como argumentos.  
  
 Al igual que la función OPENROWSET, OPENDATASOURCE solo debe hacer referencia a orígenes de datos OLE DB a los que se tiene acceso con poca frecuencia. Defina un servidor vinculado para los orígenes de datos a los que tiene acceso varias veces. Ni OPENDATASOURCE ni OPENROWSET proporcionan toda la funcionalidad de definiciones de servidores vinculados, como la administración de seguridad y la capacidad de consultar información de catálogos. Toda la información de conexión, incluidas las contraseñas, se debe proporcionar siempre que se llama OPENDATASOURCE.  
  
> [!IMPORTANT]  
>  La autenticación de Windows es mucho más segura que la de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Siempre que sea posible, debe utilizar la Autenticación de Windows. OPENDATASOURCE no se debe utilizar con contraseñas explícitas en la cadena de conexión.  
  
 Los requisitos de conexión de cada proveedor son similares a los requisitos de esos parámetros cuando se crean servidores vinculados. En el artículo [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) se incluye información detallada sobre muchos proveedores comunes.  
  
 Las llamadas a OPENDATASOURCE, OPENQUERY u OPENROWSET en la cláusula FROM se evalúan por separado y de forma independiente de otras llamadas a estas funciones utilizadas como destino de la actualización, incluso si se han suministrado argumentos idénticos a las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
## <a name="permissions"></a>Permisos  
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
  
## <a name="see-also"></a>Consulte también  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
