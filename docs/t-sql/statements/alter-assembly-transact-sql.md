---
title: ALTER ASSEMBLY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs: TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
caps.latest.revision: "76"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b1a0a6da27bc534e22da2995fa592d6b430d418
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica una ensamblado cambiando las propiedades del catálogo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de un ensamblado. ALTER ASSEMBLY lo actualiza a la última copia de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] módulos que conservan su implementación y agrega o quitan los archivos asociados con él. Los ensamblados se crean mediante el uso de [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  

>  [!WARNING]
>  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. Un ensamblado CLR creado con la opción `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios sysadmin. A partir de [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción `clr strict security` está habilitada de forma predeterminada y trata los ensamblados `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Microsoft recomienda que todos los ensamblados estén firmados con un certificado o clave asimétrica con el correspondiente inicio de sesión que tenga concedido el permiso `UNSAFE ASSEMBLY` en la base de datos maestra. Para obtener más información, vea [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md).  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *ASSEMBLY_NAME*  
 Es el nombre del ensamblado que se desea modificar. *ASSEMBLY_NAME* ya debe existir en la base de datos.  
  
 DESDE \<client_assembly_specifier > | \<assembly_bits >  
 Actualiza un ensamblado a la última copia de los módulos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que conservan su implementación. Esta opción solo se puede utilizar si no hay archivos asociados con el ensamblado especificado.  
  
 \<client_assembly_specifier > especifica la red o ubicación local donde se encuentra el ensamblado que se está actualizando. La ubicación de red incluye el nombre del equipo, el nombre del recurso compartido y una ruta dentro de ese recurso compartido. *manifest_file_name* especifica el nombre del archivo que contiene el manifiesto del ensamblado.  
  
 \<assembly_bits > es el valor binario para el ensamblado.  
  
 Deben generarse instrucciones ALTER ASSEMBLY independientes para cada ensamblado dependiente que también debe actualizarse.  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
>  [!IMPORTANT]  
>  El `PERMISSION_SET` opción se ve afectada por la `clr strict security` opción, se describe en la advertencia de apertura. Cuando `clr strict security` está habilitado, todos los ensamblados se tratan como `UNSAFE`.  
 Especifica la propiedad del conjunto de permisos de acceso al código [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] del ensamblado. Para obtener más información acerca de esta propiedad, vea [CREATE ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md).  
  
> [!NOTE]  
>  Las opciones EXTERNAL_ACCESS y UNSAFE no están disponibles en una base de datos contenida.  
  
 VISIBILITY = { ON | OFF }  
 Indica si el ensamblado es visible para crear en él funciones CLR (Common Language Runtime), procedimientos almacenados, desencadenadores, tipos definidos por el usuario y funciones de agregado definidas por el usuario. Si se establece en OFF, el ensamblado se ha diseñado para que solo se lo llame con otros ensamblados. Si ya existen objetos de base de datos CLR creados en el ensamblado, la visibilidad del ensamblado no se puede cambiar. Cualquier ensamblado al que hace referencia *assembly_name* se cargan como no visibles de forma predeterminada.  
  
 UNCHECKED DATA  
 De forma predeterminada, ALTER ASSEMBLY genera errores si debe comprobar la coherencia de filas de tabla individuales. Esta opción permite posponer las comprobaciones para más adelante con DBCC CHECKTABLE. Si se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta la instrucción ALTER ASSEMBLY aunque existan tablas en la base de datos que contienen lo siguiente:  
  
-   Columnas calculadas persistentes que hacen referencia de forma directa o indirecta a métodos en el ensamblado, mediante funciones o métodos de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Restricciones CHECK que hacen referencia de forma directa o indirecta a métodos en el ensamblado.  
  
-   Columnas de un tipo definido por el usuario CLR que dependan del ensamblado y el tipo implementa una **UserDefined** (no -**nativo**) formato de serialización.  
  
-   Columnas de un tipo definido por el usuario CLR que hacen referencia a vistas creadas con WITH SCHEMABINDING.  
  
 Si está presente alguna restricción CHECK, se deshabilita y se marca sin confianza. Las tablas que contienen columnas que dependen del ensamblado se marcan como que contienen datos sin comprobar hasta que se comprueban explícitamente.  
  
 Solo los miembros de la **db_owner** y **db_ddlowner** roles fijos de base de datos pueden especificar esta opción.  
  
 Requiere la **ALTER ANY SCHEMA** permiso para especificar esta opción.  
  
 Para obtener más información, consulte [implementar ensamblados](../../relational-databases/clr-integration/assemblies-implementing.md).  
  
 [DROP FILE { *file_name*[ **,***.. .n*] | ALL}]  
 Quita de la base de datos el nombre de archivo o todos los archivos asociados con el ensamblado. Si se utiliza con ADD FILE a continuación, primero se ejecuta DROP FILE. Esto le permite reemplazar un archivo con el mismo nombre de archivo.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 [ADD FILE FROM { *client_file_specifier* [AS *file_name*] | *file_bits*AS *file_name*}  
 Carga un archivo que se asociará con el ensamblado, por ejemplo, el código fuente, depurar archivos u otros información relacionada, en el servidor y se hace visible en el **sys.assembly_files** vista de catálogo. *client_file_specifier* especifica la ubicación desde la que se va a cargar el archivo. *file_bits* puede utilizarse en su lugar para especificar la lista de valores binarios que componen el archivo. *file_name* especifica el nombre en la que el archivo debe almacenarse en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *file_name* debe especificarse si *file_bits* se especifica y es opcional si *client_file_specifier* se especifica. Si *file_name* no se especifica, la parte file_name de *client_file_specifier* se utiliza como *file_name*.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
## <a name="remarks"></a>Comentarios  
 ALTER ASSEMBLY no interrumpe las sesiones en ejecución actuales que están ejecutando código en el ensamblado que se va a modificar. Las sesiones actuales completan su ejecución utilizando los bits no modificados del ensamblado.  
  
 Si se especifica la cláusula FROM, ALTER ASSEMBLY actualiza el ensamblado en relación con las últimas copias de los módulos proporcionados. Puesto que pueden existir funciones CLR, procedimientos almacenados, desencadenadores, tipos de datos y funciones de agregado definidas por el usuario en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya definidas en el ensamblado, la instrucción ALTER ASSEMBLY las vuelve a enlazar con la última implementación del ensamblado. Para realizar la operación de volver a enlazar, los métodos que asignan a funciones CLR, procedimientos almacenados y desencadenadores ya deben existir en el ensamblado modificado con las mismas firmas. Las clases que implementan tipos definidos por el usuario CLR y funciones de agregado definidas por el usuario deben cumplir los requisitos de ser un tipo o un agregado definido por el usuario.  
  
> [!CAUTION]  
>  Si no se especifica WITH UNCHECKED DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará evitar que ALTER ASSEMBLY se ejecute si la nueva versión de ensamblado afecta a los datos existentes de tablas, índices u otros sitios permanentes. No obstante, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza que las columnas, las vistas indizadas, las expresiones o los índices calculados serán coherentes con las rutinas y los tipos subyacentes cuando se actualice el ensamblado CLR. Al ejecutar ALTER ASSEMBLY, tenga cuidado de que no se produzcan discrepancias entre el resultado de una expresión y los valores basados en esa expresión que se almacenen en el ensamblado.  
  
 ALTER ASSEMBLY cambia la versión de ensamblado. La referencia cultural y el símbolo (token) de clave pública del ensamblado siguen siendo los mismos.  
  
 La instrucción ALTER ASSEMBLY no se puede usar para cambiar lo siguiente:  
  
-   Las firmas de funciones CLR, procedimientos almacenados y desencadenadores en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hace referencia al ensamblado. ALTER ASSEMBLY genera errores cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede volver a enlazar objetos de base de datos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la nueva versión del ensamblado.  
  
-   Las firmas de métodos en el ensamblado que se llaman desde otros ensamblados.  
  
-   La lista de ensamblados que dependen del ensamblado, como se hace referencia en el **DependentList** propiedad del ensamblado.  
  
-   La posibilidad de indización de un método, a menos que no existan índices o columnas calculadas persistentes que dependan de ese método, de forma directa o indirecta.  
  
-   El **FillRow** atributo de nombre de método para las funciones con valores de tabla CLR.  
  
-   El **Accumulate** y **Terminate** firma de método para agregados definidos por el usuario.  
  
-   Ensamblados del sistema.  
  
-   Propiedad del ensamblado. Use [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md) en su lugar.  
  
 Además, para ensamblados que implementan tipos definidos por el usuario, se puede utilizar ALTER ASSEMBLY para realizar solo los siguientes cambios:  
  
-   Modificar métodos públicos de la clase de tipo definido por el usuario, siempre que no se modifiquen firmas ni atributos.  
  
-   Agregar nuevos métodos públicos.  
  
-   Modificar métodos privados de cualquier manera.  
  
 Campos incluidos en un serialización nativa definido por el usuario tipo, incluidos los miembros de datos o clases base, no se puede cambiar mediante el uso de ALTER ASSEMBLY. No se admiten otros cambios.  
  
 Si no se especifica ADD FILE FROM, ALTER ASSEMBLY quita los archivos asociados con el ensamblado.  
  
 Si se ejecuta ALTER ASSEMBLY sin la cláusula de datos UNCHECKED, se realizan comprobaciones para comprobar que la nueva versión del ensamblado no afecta a los datos existentes en las tablas. Dependiendo de la cantidad de datos que sea necesario comprobar, puede afectar al rendimiento.  
  
## <a name="permissions"></a>Permissions  
 Se requiere el permiso ALTER en el ensamblado. Algunos requisitos adicionales son los siguientes:  
  
-   Para modificar un ensamblado cuyo permiso existente es EXTERNAL_ACCESS conjunto, requiere**EXTERNAL ACCESS ASSEMBLY**permiso en el servidor.  
  
-   Para modificar un ensamblado cuyo permiso existente conjunto es UNSAFE requiere **ENSAMBLADO UNSAFE** permiso en el servidor.  
  
-   Para cambiar el conjunto de permisos de un ensamblado a EXTERNAL_ACCESS, requiere**EXTERNAL ACCESS ASSEMBLY** permiso en el servidor.  
  
-   Para cambiar el conjunto de permisos de un ensamblado a UNSAFE, es necesario **ENSAMBLADO UNSAFE** permiso en el servidor.  
  
-   Si se especifica WITH UNCHECKED DATA, requiere **ALTER ANY SCHEMA** permiso.  


### <a name="permissions-with-clr-strict-security"></a>Permisos de seguridad estricta de CLR    
Los siguientes permisos necesarios para modificar un ensamblado CLR cuando `CLR strict security` está habilitada:

- El usuario debe tener el permiso `ALTER ASSEMBLY`.  
- Además, se debe dar una de las siguientes condiciones:  
  - El ensamblado debe estar firmado con un certificado o clave asimétrica que tenga el inicio de sesión correspondiente con el permiso `UNSAFE ASSEMBLY` en el servidor. Se recomienda firmar el ensamblado.  
  - La base de datos tiene la propiedad `TRUSTWORTHY` establecida en `ON` y pertenece a un inicio de sesión que tiene el permiso `UNSAFE ASSEMBLY` en el servidor. Esta opción no se recomienda.  
  
  
 Para obtener más información acerca de los conjuntos de permisos de ensamblado, consulte [diseñar ensamblados](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-refreshing-an-assembly"></a>A. Actualizar un ensamblado  
 En el siguiente ejemplo se actualiza el ensamblado `ComplexNumber` a la última copia de los módulos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que conservan su implementación.  
  
> [!NOTE]  
>  El ensamblado `ComplexNumber` se puede crear ejecutando los scripts de ejemplo UserDefinedDataType. Para obtener más información, consulte [User Defined Type](http://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191).  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```
### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>B. Agregar una archivo para asociarlo con el ensamblado  
 En el siguiente ejemplo se carga el archivo de código de origen `Class1.cs` para asociarlo con el ensamblado `MyClass`. En este ejemplo se asume que el ensamblado `MyClass` ya está creado en la base de datos.  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  
  
### <a name="c-changing-the-permissions-of-an-assembly"></a>C. Cambiar los permisos de un ensamblado  
 En el ejemplo siguiente se cambia el conjunto de permisos del ensamblado `ComplexNumber` de SAFE a `EXTERNAL ACCESS`.  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR ENSAMBLADOS &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ELIMINAR ENSAMBLADOS &#40; Transact-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
