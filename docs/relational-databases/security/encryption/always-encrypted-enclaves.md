---
title: Always Encrypted con enclaves seguros (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 377c2d95564e7348bdfb5de9480c7c7f5004c7f7
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938161"
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
> En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], los cálculos completos tienen pendientes varias optimizaciones de rendimiento, incluida la funcionalidad limitada (sin indexación, etc.), y actualmente están deshabilitados de manera predeterminada. Para habilitar los cálculos completos, consulte la sección sobre cómo [habilitar los cálculos completos](configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], Always Encrypted con enclaves seguros usa enclaves seguros de memoria de [Seguridad basada en virtualización (VBS)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) (también conocidos como enclaves de Modo seguro virtual, VSM) en Windows.

## <a name="secure-enclave-attestation"></a>Atestación de un enclave seguro

El enclave seguro dentro del motor de SQL Server puede acceder a información confidencial almacenada en columnas de bases de datos cifradas y las claves de cifrado de columna correspondientes en texto no cifrado. Antes de enviar a SQL Server una consulta que implica cálculos de enclave, el controlador cliente dentro de la aplicación debe comprobar que el enclave seguro es un enclave genuino basado en una tecnología determinada (por ejemplo, VBS) y que el código que se ejecuta dentro del enclave se confirmó para ejecución dentro del enclave. 

El proceso de comprobar el enclave se denomina **atestación del enclave** y, por lo general, implica que un controlador cliente dentro de la aplicación (y, a veces, también SQL Server) se ponga en contacto con un servicio de atestación externo. Los detalles específicos del proceso de atestación dependen de la tecnología del enclave y del servicio de atestación.

El proceso de atestación que SQL Server admite para los enclaves seguros de VBS en [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] es la atestación de entorno de ejecución Protección del sistema de Windows Defender, que usa Servicio de protección de host (HGS) como servicio de atestación. Deberá configura HGS en su entorno y registrar la máquina que hospeda la instancia de SQL Server en HGS. También debe configurar las herramientas o aplicaciones cliente (por ejemplo, SQL Server Management Studio) con una atestación de HGS.

## <a name="secure-enclave-providers"></a>Proveedores de enclaves seguros

Para usar Always Encrypted con enclaves seguros, una aplicación debe usar un controlador cliente que admita la característica. En [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], las aplicaciones deben usar Proveedor de datos .NET Framework 4.7.2 y .NET Framework para SQL Server. Además, las aplicaciones .NET se deben configurar con un **proveedor de enclaves seguros** específico para el tipo de enclave (por ejemplo VBS) y el servicio de atestación (por ejemplo, HGS) que usa. Los proveedores de enclaves admitidos se envían por separado en un paquete NuGet, el que debe integrar con su aplicación. Un proveedor de enclaves implementa la lógica del cliente para el protocolo de atestación y para establecer un canal seguro con un enclave seguro de un tipo determinado.

## <a name="enclave-enabled-keys"></a>Claves habilitadas para el enclave

Always Encrypted con enclaves seguros presenta el concepto de las claves habilitadas para el enclave:

- **Clave maestra de columna habilitada para el enclave**: una clave maestra de columna que tiene la propiedad ENCLAVE_COMPUTATIONS especificada en el objeto de metadatos de clave maestra de columna dentro de la base de datos. El objeto de metadatos de clave maestra de columna también debe contener una signatura válida de las propiedades de los metadatos.
- **Clave de cifrado de columna habilitada para el enclave**: una clave de cifrado de columna cifrada con una clave maestra de columna habilitada para el enclave.

Cuando el motor de SQL Server determina las operaciones, especificadas en una consulta, que se deben realizar dentro del enclave seguro, el motor de SQL Server solicita que el controlador cliente comparta las claves de cifrado de columna que se necesitan para los cálculos con el enclave seguro. El controlador cliente comparte las claves de cifrado de columna solo si las claves están habilitadas para el enclave (es decir, si están cifradas con claves maestras de columna habilitadas para el enclave) y que tengan una signatura válida. En caso contrario, se generará un error en la consulta.

## <a name="enclave-enabled-columns"></a>Columnas habilitadas para el enclave

Una columna habilitada para el enclave es una columna de base de datos cifrada con una clave de cifrado de columna habilitada para el enclave. La funcionalidad disponible para una columna habilitada para el enclave depende del tipo de cifrado que usa la columna.

- **Cifrado determinista**: las columnas habilitadas para el enclave que usan el cifrado determinista admiten el cifrado en contexto, pero ninguna otra operación dentro del enclave seguro. Se admite la comparación de igualdad, pero se realiza fuera del enclave mediante la comparación del texto cifrado (fuera del enclave).  
- **Cifrado aleatorio**: las columnas habilitadas para el enclave que usan el cifrado aleatorio admiten el cifrado en contexto, al igual que los cálculos completos, dentro del enclave seguro. Los cálculos completos son la coincidencia de patrones y los [operadores de comparación](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql), incluida la comparación de igualdad.

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

## <a name="known-limitations"></a>Restricciones conocidas

Limitaciones generales: 

- Todas las limitaciones que se muestran para la versión actual de Always Encrypted en [Detalles de las características](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details) también se aplican a Always Encrypted con enclaves seguros (a las columnas cifradas con claves habilitadas para el enclave), a excepción de las restricciones que se quitan al agregar compatibilidad para el cifrado en contexto y los cálculos completos.

- La comparación de igualdad sigue siendo el mismo operador Transact-SQL que se admite con el cifrado determinista y las comparaciones de igualdad se realizan al comparar los valores de texto cifrado fuera del enclave, independientemente de si la clave de cifrado de columnas está habilitada o no para el enclave. La única funcionalidad nueva que se desbloquea con las claves de cifrado de columna habilitadas para el enclave para el cifrado determinista son las operaciones criptográficas en contexto. Si tiene una columna que se cifró con el cifrado determinista (y una clave no habilitada para el enclave), para habilitar los cálculos completos (coincidencia de patrones, operaciones de comparación), debe volver a cifrar la columna mediante el cifrado aleatorio.

- La restricción existente sobre el uso de intercalaciones se aplica a las columnas cifradas con claves de cifrado de columna habilitadas para el enclave: las columnas de cadena de caracteres (char, nchar, varchar, nvarchar) cifradas mediante el cifrado determinista deben usar intercalaciones con un criterio de ordenación BINARY2 (intercalaciones BIN2). Las columnas de cadena de caracteres que usan intercalaciones que no son BIN2 se pueden cifrar mediante el cifrado aleatorio, pero la única funcionalidad que está habilitada para dichas columnas (si están cifradas con claves de cifrado de columna habilitadas para el enclave) es el cifrado en contexto. **Para admitir los cálculos completos (coincidencia de patrones, operaciones de comparación), una columna debe usar una intercalación BIN2** (y la columna se debe cifrar con el cifrado aleatorio y una clave de cifrado de columna habilitada para el enclave).

- No se admite el uso de claves habilitadas para enclave en las columnas en tablas en memoria.

- Las operaciones criptográficas en contexto no se pueden combinar con ningún otro cambio de metadatos de columna, excepto los cambios de intercalación y nulabilidad. Por ejemplo, no puede cifrar, volver a cifrar ni descifrar una columna Y cambiar un tipo de datos de la columna en una sola instrucción Transact-SQL ALTER TABLE o ALTER COLUMN. Debe usar dos instrucciones independientes.

Estas limitaciones se aplican a la versión preliminar actual, pero están programadas para solucionarlas:

- No es posible indexar las columnas habilitadas para el enclave con cifrados aleatorios, lo que significa que las operaciones de comparación o las operaciones LIKE requieren recorridos de tabla.

- El único controlador cliente que admite Always Encrypted con enclaves seguros es Proveedor de datos .NET Framework para SQL Server (ADO.NET) en .NET Framework 4.7.2. No hay compatibilidad para ODBC/JDBC.

- Los únicos almacenes de claves que se admiten para almacenar claves maestras de columna habilitadas para el enclave son Almacén de certificados de Windows y Azure Key Vault.

- La compatibilidad de herramientas para Always Encrypted con enclaves seguros actualmente es incompleta. Para desencadenar una operación criptográfica en contexto a través de una instrucción Transact-SQL ALTER TABLE, debe emitir la instrucción mediante una ventana de consulta en SSMS, o bien puede escribir su propio programa que emita la instrucción. El cmdlet Set-SqlColumnEncryption en el módulo SqlServer de PowerShell y el Asistente para Always Encrypted en SQL Server Management Studio todavía no admiten el cifrado en contexto, pero actualmente hay herramientas que sacan los datos de la base de datos para realizar operaciones criptográficas, incluso si las claves de cifrado de columna que se usan en las operaciones están habilitadas para el enclave. 

## <a name="known-issues"></a>Problemas conocidos

- Los cálculos completos que se hacen en columnas de cadena no UNICODE (char, varchar) requieren que haya una intercalación BIN2 establecida en el nivel de base de datos. Consulte las consideraciones especiales para columnas de cadena no UNICODE en [Administrar intercalaciones](configure-always-encrypted-enclaves.md#manage-collations).

## <a name="next-steps"></a>Next Steps

- Configure un entorno de prueba y pruebe la funcionalidad de Always Encrypted con enclaves seguros en SSMS, vea [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).
