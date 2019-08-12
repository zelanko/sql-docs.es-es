---
title: Always Encrypted con enclaves seguros (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 22570f7ae8a9f11b89f11027698c948be5766d25
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661227"
---
# <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

 
Always Encrypted con enclaves seguros proporciona funcionalidad adicional a la característica [Always Encrypted](always-encrypted-database-engine.md).

Introducido en SQL Server 2016, Always Encrypted protege la privacidad de la información confidencial contra malware y usuarios *no autorizados* de SQL Server con privilegios elevados. Los usuarios no autorizados con privilegios elevados son administradores de bases de datos, administradores de equipos, administradores de nube o cualquier otro usuario con acceso legítimo a las instancias de servidor, hardware, etc., pero que no deberían tener acceso a parte ni a la totalidad de los datos reales. 

Para proteger los datos, Always Encrypted hasta ahora los cifrada en el cliente y no permitía que los datos ni las claves criptográficas correspondientes aparecieran en texto no cifrado dentro del motor de SQL Server. Como resultado, la funcionalidad en columnas cifradas dentro de la base de datos era muy restringida. Las únicas operaciones que SQL Server podía realizar en datos cifrados eran comparaciones de igualdad (y las comparaciones de igualdad solo estaban disponibles con cifrado determinista). Todas las demás operaciones, incluidas las operaciones criptográficas (el cifrado inicial de los datos o la rotación de claves) o los cálculos completos (por ejemplo, la coincidencia de patrones) no se admitían dentro de la base de datos. Los usuarios tenían que sacar los datos de la base de datos para llevar a cabo estas operaciones en el cliente.

Always Encrypted *con enclaves seguros* aborda estas limitaciones al permitir realizar cálculos en datos de texto no cifrado dentro de un enclave seguro en el servidor. Un enclave seguro es una región de memoria protegida dentro del proceso de SQL Server y sirve como un entorno de ejecución de confianza para procesar información confidencial dentro del motor de SQL Server. Un enclave seguro aparece como una caja negra para el resto de SQL Server y otros procesos en la máquina servidor. No hay ninguna manera de ver los datos ni el código que se encuentran dentro del enclave desde el exterior, incluso si se cuenta con un depurador.  


Always Encrypted usa enclaves seguros, tal como se muestra en el siguiente diagrama:

![flujo de datos](./media/always-encrypted-enclaves/ae-data-flow.png)



Al analizar la consulta de una aplicación, el motor de SQL Server determina si la consulta contiene alguna operación realizada en datos cifrados que requiere usar el enclave seguro. En el caso de consultas en las que se debe acceder al enclave seguro:

- El controlador cliente envía las claves de cifrado de columna que se requieren para las operaciones al enclave seguro (a través de un canal seguro). 
- Luego, el controlador cliente envía la consulta para su ejecución junto con los parámetros de la consulta cifrada.

Durante el procesamiento de la consulta, las claves de cifrado de la columna o los datos no se exponen como texto no cifrado en el motor de SQL Server fuera del enclave seguro. El motor de SQL Server delega los cálculos y las operaciones criptográficas en columnas cifradas al enclave seguro. Si es necesario, el enclave seguro descifra los parámetros de la consulta y los datos almacenados en las columnas cifradas y lleva a cabo las operaciones solicitadas.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>¿Por qué usar Always Encrypted con enclaves seguros?

Con los enclaves seguros, Always Encrypted protege la privacidad de la información confidencial mientras se brindan estas ventajas:

- **Cifrado en contexto**: las operaciones criptográficas sobre información confidencial, como el cifrado inicial de datos o la rotación de una clave de cifrado de columna, se realizan dentro del enclave seguro y no requieren sacar los datos de la base de datos. Puede genera cifrado en contexto con la instrucción Transact-SQL ALTER TABLE y no es necesario usar herramientas, como el Asistente para Always Encrypted en SSMS o el cmdlet Set-SqlColumnEncryption de PowerShell.

- **Cálculos completos (versión preliminar)** : las operaciones sobre columnas cifradas, incluidas la coincidencia de patrones (el predicado LIKE) y las comparaciones de variedades, se admiten dentro del enclave seguro, que permite que Always Encrypted se use en una amplia variedad de aplicaciones y escenarios que requiere que dichos cálculos se realicen dentro del sistema de la base de datos.

> [!IMPORTANT]
> En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], los cálculos completos son varias optimizaciones de rendimiento pendientes y mejoras en el control de errores, y actualmente están deshabilitados de forma predeterminada. Para habilitar los cálculos completos, consulte la sección sobre cómo [habilitar los cálculos completos](configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], Always Encrypted con enclaves seguros usa enclaves seguros de memoria de [Seguridad basada en virtualización (VBS)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) (también conocidos como enclaves de Modo seguro virtual, VSM) en Windows.

## <a name="secure-enclave-attestation"></a>Atestación de un enclave seguro

El enclave seguro dentro del motor de SQL Server puede acceder a información confidencial almacenada en columnas de bases de datos cifradas y las claves de cifrado de columna correspondientes en texto no cifrado. Antes de enviar a SQL Server una consulta que implica cálculos de enclave, el controlador cliente dentro de la aplicación debe comprobar que el enclave seguro es un enclave genuino basado en una tecnología determinada (por ejemplo, VBS) y que el código que se ejecuta dentro del enclave se confirmó para ejecución dentro del enclave. 

El proceso de comprobar el enclave se denomina **atestación del enclave** y, por lo general, implica que un controlador cliente dentro de la aplicación y SQL Server se pongan en contacto con un servicio de atestación externo. Los detalles específicos del proceso de atestación dependen de la tecnología del enclave y del servicio de atestación.

El proceso de atestación que SQL Server admite para los enclaves seguros de VBS en [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] es la atestación de entorno de ejecución Protección del sistema de Windows Defender, que usa Servicio de protección de host (HGS) como servicio de atestación. Deberá configura HGS en su entorno y registrar la máquina que hospeda la instancia de SQL Server en HGS. También debe configurar las herramientas o aplicaciones cliente (por ejemplo, SQL Server Management Studio) con una atestación de HGS.

## <a name="secure-enclave-providers"></a>Proveedores de enclaves seguros

Para usar Always Encrypted con enclaves seguros, una aplicación debe usar un controlador cliente que admita la característica. En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], las aplicaciones deben usar Proveedor de datos .NET Framework 4.7.2 y .NET Framework para SQL Server. Además, las aplicaciones .NET se deben configurar con un **proveedor de enclaves seguros** específico para el tipo de enclave (por ejemplo VBS) y el servicio de atestación (por ejemplo, HGS) que usa. Los proveedores de enclaves admitidos se envían por separado en un paquete NuGet, el que debe integrar con su aplicación. Un proveedor de enclaves implementa la lógica del cliente para el protocolo de atestación y para establecer un canal seguro con un enclave seguro de un tipo determinado.

## <a name="enclave-enabled-keys"></a>Claves habilitadas para el enclave

Always Encrypted con enclaves seguros presenta el concepto de las claves habilitadas para el enclave:

- **Clave maestra de columna habilitada para el enclave**: una clave maestra de columna que tiene la propiedad ENCLAVE_COMPUTATIONS especificada en el objeto de metadatos de clave maestra de columna dentro de la base de datos. El objeto de metadatos de clave maestra de columna también debe contener una signatura válida de las propiedades de los metadatos.
- **Clave de cifrado de columna habilitada para el enclave**: una clave de cifrado de columna cifrada con una clave maestra de columna habilitada para el enclave.

Cuando el motor de SQL Server determina las operaciones, especificadas en una consulta, que se deben realizar dentro del enclave seguro, el motor de SQL Server solicita que el controlador cliente comparta las claves de cifrado de columna que se necesitan para los cálculos con el enclave seguro. El controlador cliente comparte las claves de cifrado de columna solo si las claves están habilitadas para el enclave (es decir, si están cifradas con claves maestras de columna habilitadas para el enclave) y están firmadas correctamente. En caso contrario, se generará un error en la consulta.

## <a name="enclave-enabled-columns"></a>Columnas habilitadas para el enclave

Una columna habilitada para el enclave es una columna de base de datos cifrada con una clave de cifrado de columna habilitada para el enclave. La funcionalidad disponible para una columna habilitada para el enclave depende del tipo de cifrado que usa la columna.

- **Cifrado determinista**: las columnas habilitadas para el enclave que usan el cifrado determinista admiten el cifrado en contexto, pero ninguna otra operación dentro del enclave seguro. Se admite la comparación de igualdad, pero se realiza fuera del enclave mediante la comparación del texto cifrado.  
- **Cifrado aleatorio**: las columnas habilitadas para el enclave que usan el cifrado aleatorio admiten el cifrado en contexto, al igual que los cálculos completos, dentro del enclave seguro. Los cálculos completos son la coincidencia de patrones y los [operadores de comparación](../../../t-sql/language-elements/comparison-operators-transact-sql.md), incluida la comparación de igualdad.

Para más información sobre los tipos de cifrado, consulte [Criptografía de Always Encrypted](always-encrypted-cryptography.md).

En la tabla siguiente se resume la funcionalidad disponible para las columnas cifradas, en función de si las columnas usan claves de cifrado de columna habilitadas para el enclave y un tipo de cifrado.

| **Operación**| **La columna NO está habilitada para el enclave** |**La columna NO está habilitada para el enclave**| **La columna está habilitada para el enclave**  |**La columna está habilitada para el enclave** |
|:---|:---|:---|:---|:---|
| | **Cifrado aleatorio**  | **Cifrado determinista**     | **Cifrado aleatorio**      | **Cifrado determinista**     |
| **Cifrado en contexto** | No admitida  | No admitida   | Admitida         | Admitida    |
| **Comparación de igualdad**   | No admitida | Admitida fuera del enclave | Admitida (dentro del enclave) | Admitida fuera del enclave |
| **Operadores de comparación más allá de la igualdad** | No admitida  | No admitida   | Admitida      | No admitida     |
| **LIKE**    | No admitida      | No admitida    | Admitida     | No admitida    |

El cifrado en contexto incluye compatibilidad con estas operaciones dentro del enclave:

- Cifrado inicial de los datos almacenados en una columna existente.
- Nuevo cifrado de los datos existentes en una columna, por ejemplo:
  
  - Rotación de la clave de cifrado de columna (nuevo cifrado de la columna con otra clave).
  - Cambio del tipo de cifrado.  

- Descifrado de los datos almacenados en una columna cifrada (conversión de la columna en una columna de texto no cifrado).

Para que se realice un cifrado en contexto, la clave (o claves) de cifrado de columna que participa en las operaciones criptográficas debe estar habilitada para el enclave:

- Cifrado inicial: la clave de cifrado de columna para la columna que se está cifrando debe estar habilitada para el enclave.
- Nuevo cifrado: tanto la clave de cifrado de columna actual como la de destino (si es distinta de la actual) deben estar habilitadas para el enclave.
- Descifrado: la clave de cifrado de columna actual de la columna debe estar habilitada para el enclave.

### <a name="indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Índices en columnas habilitadas para enclave mediante cifrado aleatorio
Puede crear índices no agrupados en columnas habilitadas para enclave mediante cifrado aleatorio con el fin de acelerar la ejecución de consultas completas. Para tener la seguridad de que un índice en una columna cifrada mediante cifrado aleatorio no pierda datos confidenciales y, al mismo tiempo, sea útil para procesar las consultas dentro del enclave, los valores de clave de la estructura de datos de índice (árbol B) se cifran y se ordenan según sus valores de texto no cifrado. Cuando el ejecutor de consultas del motor de SQL Server utiliza un índice en una columna cifrada para realizar cálculos dentro del enclave, busca el índice para consultar valores específicos almacenados en la columna. Cada búsqueda puede suponer varias comparaciones. El ejecutor de consultas delega cada comparación en el enclave, que descifra un valor almacenado en la columna y el valor del índice cifrado que se va a comparar, realiza la comparación en texto sin cifrar y devuelve el resultado de la comparación al ejecutor. Para obtener información general, no específica de Always Encrypted, acerca de cómo funciona la indexación en SQL Server, consulte [Índices agrupados y no agrupados descritos](../../indexes/clustered-and-nonclustered-indexes-described.md).

Como un índice en una columna habilitada para enclave que usa cifrado aleatorio almacena los valores de clave de índice cifrados mientras se ordenan en función de texto sin cifrar, el motor de SQL Server debe usar el enclave en cualquier operación que suponga la creación o actualización de un índice, por ejemplo:
- Creación o recompilación de un índice.
- Inserción, actualización o eliminación de una fila de la tabla (que contiene una columna indexada o cifrada), que desencadena la inserción o eliminación de una clave de índice hacia y desde el índice.
- Ejecución de comandos DBCC que implican la comprobación de la integridad de los índices, por ejemplo [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) o [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
- Recuperación de base de datos (por ejemplo, después de que SQL Server produce un error y se reinicia), si SQL Server necesita deshacer los cambios realizados en el índice (consulte más detalles a continuación).

Para todas las operaciones anteriores, es necesario que el enclave tenga la clave de cifrado de columna de la columna indexada, de forma que pueda descifrar las claves de índice. En general, el enclave puede obtener una clave de cifrado de columna de una de dos maneras:

- **Directamente desde la aplicación cliente** que invoca la operación en el índice, como se describe en la introducción anterior. Con este método es necesario que la aplicación o el usuario tengan acceso a la clave maestra de columna y a la clave de cifrado de columna, que protegen la columna indexada. La aplicación debe conectarse a la base de datos con Always Encrypted habilitado para la conexión.
- **Desde la caché de claves de cifrado de columna.** El enclave almacena las claves usadas en las consultas anteriores en la caché que se encuentra dentro del enclave y, por lo tanto, no es accesible desde el exterior. Si una aplicación desencadena una operación en un índice sin proporcionar la clave de cifrado de columna necesaria directamente, el enclave busca la clave en la caché. Si el enclave encuentra la clave en la caché, la usa para la operación. Este método permite que los administradores de base de datos (DBA) administren los índices y realicen determinadas operaciones de limpieza de los datos (por ejemplo, quitar una fila de una tabla que contiene un índice en una columna cifrada), sin tener acceso a las claves criptográficas o a los datos en texto sin cifrar. Para usarlo, es necesario que la aplicación se conecte a la base de datos sin Always Encrypted habilitado para la conexión.

Sigue sin ser posible la creación de índices en columnas que usan cifrado aleatorio y no están habilitadas para el enclave.

#### <a name="database-recovery"></a>Recuperación de la bases de datos

Si se produce un error en una instancia de SQL Server, sus bases de datos pueden quedar en un estado donde los archivos de datos pueden contener algunas modificaciones por transacciones incompletas. Cuando se inicia la instancia, se ejecuta un proceso denominado [recuperación de bases de datos](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started), que supone revertir las transacciones incompletas encontradas en el registro de transacciones para asegurarse de que se preserva la integridad de la base de datos. Si una transacción incompleta realizó algún cambio en un índice, puede que también sea necesario deshacer esos cambios. Por ejemplo, puede que haya que quitar o volver a insertar algunos valores de clave del índice.

> [!IMPORTANT]
> Microsoft recomienda encarecidamente habilitar la [recuperación de base de datos acelerada (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) para la base de datos **antes** de crear el primer índice en una columna habilitada para enclave que se ha cifrado con cifrado aleatorio.

Con el [proceso de recuperación de base de datos tradicional](https://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (que sigue al modelo de recuperación [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)), para deshacer un cambio en un índice, SQL Server debe esperar a que una aplicación proporcione la clave de cifrado de la columna al enclave, lo que puede tardar mucho tiempo. ADR reduce enormemente el número de operaciones de deshacer que se debe aplazar porque una clave de cifrado de columna no está disponible en la caché dentro del enclave. Por lo tanto, aumenta considerablemente la disponibilidad de la base de datos, ya que reduce la posibilidad de que una nueva transacción se bloquee. Con ADR habilitado, SQL Server puede seguir necesitando una clave de cifrado de columna para completar la limpieza de las versiones de datos antiguas, pero se haría como una tarea en segundo plano que no afecta a la disponibilidad de la base de datos o a las transacciones del usuario. Sin embargo, puede que vea mensajes de error en el registro de errores, que indican operaciones de limpieza incorrectas debido a que falta una clave de cifrado de columna.

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>Índices en columnas habilitadas para enclave mediante cifrado determinista

Un índice en una columna que usa cifrado determinista se ordena según el texto cifrado (no texto sin cifrar), sin importar si la columna está o no habilitada para enclave.

## <a name="security-considerations"></a>Consideraciones de seguridad

Se aplican las siguientes consideraciones de seguridad a Always Encrypted con enclaves seguros.

- La seguridad de los datos en el enclave depende de un protocolo de atestación y un servicio de atestación. Por lo tanto, debe asegurarse de que el servicio de atestación y las directivas de atestación, que impone el servicio, sean administrados por un administrador de confianza. Además, los servicios de atestación suelen admitir distintas directivas y protocolos de atestación, algunos de los cuales realizan la comprobación mínima del enclave y su entorno, y están diseñados para desarrollo y pruebas. Siga atentamente las directrices específicas para el servicio de atestación a fin de asegurarse de que usa las directivas y configuraciones recomendadas para sus implementaciones en producción. 
- El cifrado de una columna mediante cifrado aleatorio con una CEK habilitada para enclave puede dar lugar a una pérdida del orden de los datos almacenados en la columna, dado que tales columnas admiten comparaciones de intervalos. Por ejemplo, si una columna cifrada, que contiene los salarios de los empleados, tiene un índice, un administrador de base de datos malintencionado podría examinar el índice para buscar el valor cifrado de salario máximo e identificar a una persona con el salario máximo (suponiendo que el nombre de la persona no esté cifrado). 
- Si usa Always Encrypted para proteger datos confidenciales del acceso no autorizado por los administradores de base de datos, no comparta las claves maestras de columna ni las claves de cifrado de columna con ellos. Un administrador de base de datos puede administrar índices en columnas cifradas sin tener acceso directo a las claves, sino que aprovecha la caché de claves de cifrado de columna dentro del enclave.

## <a name="anchorname-1-considerations-availability-groups-db-migration"></a> Consideraciones sobre grupos de disponibilidad y la migración de bases de datos

Al configurar un grupo de disponibilidad Always On que es necesario para admitir consultas que usan enclaves, debe asegurarse de que todas las instancias de SQL Server que hospedan las bases de datos del grupo de disponibilidad admitan Always Encrypted con enclaves seguros y tengan un enclave configurado. Si la base de datos principal admite enclaves, pero no así una réplica secundaria, cualquier intento de usar la funcionalidad de Always Encrypted con enclaves seguros será infructuoso.

Al restaurar un archivo de copia de seguridad de una base de datos que usa la funcionalidad de Always Encrypted con enclaves seguros en una instancia de SQL Server que no tiene el enclave configurado, la operación de restauración se realizará correctamente y toda la funcionalidad que no se base en el enclave estará disponible. Sin embargo, las posteriores consultas con la funcionalidad de enclave darán error, y los índices en columnas habilitadas para enclave mediante cifrado aleatorio dejarán de ser válidos. Lo mismo se aplica al asociar una base de datos que usa Always Encrypted con enclaves seguros en la instancia que no tiene configurado el enclave.

Si la base de datos contiene índices en columnas habilitadas para enclave mediante cifrado aleatorio, asegúrese de habilitar la [recuperación de base de datos acelerada (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) en la base de datos antes de crear una copia de seguridad de base de datos. ADR garantizará que la base de datos, incluidos los índices, está disponible inmediatamente después de restaurarla. Para más información, consulte [Recuperación de la base de datos](#database-recovery).

Cuando se migra la base de datos mediante un archivo bacpac, debe asegurarse de quitar todos los índices de las columnas habilitadas para enclave con cifrado aleatorio antes de crear el archivo bacpac.

## <a name="known-limitations"></a>Restricciones conocidas

Los enclaves seguros mejoran la funcionalidad de Always Encrypted. Las siguientes funcionalidades **se admiten ahora para las columnas habilitadas para enclave**:

- Operaciones criptográficas en contexto.
- Coincidencia de patrones (LIKE) y operadores de comparación en columnas cifradas que usan cifrado aleatorio.
    > [!NOTE]
    > Las operaciones anteriores se admiten para las columnas de cadena de caracteres que se usan intercalaciones con un criterio de ordenación binary2 (intercalaciones BIN2). Las columnas de cadena de caracteres que usan intercalaciones BIN2 se pueden cifrar mediante cifrado aleatorio y claves de cifrado de columna habilitadas para enclave. Sin embargo, la única funcionalidad nueva habilitada para dichas columnas es el cifrado en contexto.
- Creación de índices no agrupados en columnas que usan cifrado aleatorio.
- Columnas calculadas mediante expresiones que contienen operadores de comparación y el predicado LIKE en columnas que usan cifrado aleatorio.

Todas las otras limitaciones (no solucionadas con las mejoras anteriores) que se enumeran para Always Encrypted (sin enclaves seguros) en [Detalles de las características](always-encrypted-database-engine.md#feature-details) también se aplican a Always Encrypted con enclaves seguros.

Las siguientes limitaciones son específicas de Always Encrypted con enclaves seguros:

- No se pueden crear índices agrupados en columnas habilitadas para enclave que usan cifrado aleatorio.
- Las columnas habilitadas para enclave que usan cifrado aleatorio no pueden ser columnas de clave principales y no se puede hacer referencia a ellas con restricciones de clave externa o restricciones de clave única.
- No se admiten combinaciones hash y combinaciones combinadas en columnas habilitadas para enclave que usan cifrado aleatorio. Solo se admiten combinaciones de bucle anidado (con índices, si están disponible).
- Las consultas con el operador LIKE o un operador de comparación que tiene un parámetro de consulta que usa uno de los siguientes tipos de datos (que se convierten en objetos grandes después del cifrado) pasan por alto los índices y realizan recorridos de tabla.
    - nchar[n] y nvarchar[n], si n es mayor que 3967.
    - char[n], varchar[n], binary[n], varbinary[n], si n es mayor que 7935.
- Las operaciones criptográficas en contexto no se pueden combinar con ningún otro cambio de metadatos de columna, excepto los cambios de intercalación dentro de la misma página de código y nulabilidad. Por ejemplo, no puede cifrar, volver a cifrar ni descifrar una columna Y cambiar un tipo de datos de la columna en una sola instrucción ALTER TABLE o ALTER COLUMN de Transact-SQL. Use dos instrucciones independientes.
- No se admite el uso de claves habilitadas para enclave en columnas de tablas en memoria.
- Los únicos almacenes de claves que se admiten para almacenar claves maestras de columna habilitadas para el enclave son Almacén de certificados de Windows y Azure Key Vault.

Las siguientes limitaciones se aplican a [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], pero están programadas para solucionarlas:

- No se admite la creación de estadísticas en columnas habilitadas para enclave que usan cifrado aleatorio.
- El único controlador cliente que admite Always Encrypted con enclaves seguros es Proveedor de datos .NET Framework para SQL Server (ADO.NET) en .NET Framework 4.7.2. No se admite ODBC/JDBC.
- La compatibilidad de herramientas para Always Encrypted con enclaves seguros actualmente es incompleta. En concreto:
  - No se admite la importación o exportación de bases de datos que contiene claves habilitadas para enclave.
  - Para desencadenar una operación criptográfica en contexto a través de una instrucción Transact-SQL ALTER TABLE, debe emitir la instrucción mediante una ventana de consulta en SSMS, o bien puede escribir su propio programa que emita la instrucción. El cmdlet Set-SqlColumnEncryption en el módulo SqlServer de PowerShell y el Asistente para Always Encrypted en SQL Server Management Studio todavía no admiten el cifrado en contexto, pero actualmente hay herramientas que sacan los datos de la base de datos para realizar operaciones criptográficas, incluso si las claves de cifrado de columna que se usan en las operaciones están habilitadas para el enclave.
- No se admiten comandos DBCC que comprueban la integridad de los índices o que los actualizan.
- Creación de índices en columnas cifradas en el momento de crear la tabla (mediante CREATE TABLE). Deberá crear un índice en una columna cifrada por separado mediante CREATE INDEX.

## <a name="next-steps"></a>Pasos siguientes

- Configure un entorno de prueba y pruebe la funcionalidad de Always Encrypted con enclaves seguros en SSMS, vea [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).
- Para obtener más información sobre cómo usar Always Encrypted con enclaves seguros, consulte [Configuración de Always Encrypted con enclaves seguros](configure-always-encrypted-enclaves.md).
