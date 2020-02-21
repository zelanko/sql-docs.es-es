---
title: Interfaz SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72cccce89d5e30a92f38b956c8b7996949d3bb46
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027701"
---
# <a name="sqlxml-interface"></a>Interfaz SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0, que presenta la interfaz java.sql.SQLXML. La interfaz SQLXML define métodos para interactuar con datos XML y manipularlos. El tipo de datos **SQLXML** se asigna al tipo de datos **xml** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
La interfaz SQLXML proporciona métodos para obtener acceso al valor XML como **String**, **Reader** o **Writer**, o como **Stream**. También se puede acceder al valor XML mediante **Source** o establecerlo como **Result**, que se usan con las API del analizador XML, como Document Object Model (DOM), Simple API for XML (SAX) y Streaming API for XML (StAX), así como con las transformaciones XSLT y con XPath.  
  
## <a name="remarks"></a>Observaciones  

La tabla siguiente describe los métodos definidos en la interfaz SQLXML:  
  
|Sintaxis del método|Descripción del método|  
|-------------------|------------------------|  
|[void free()](https://go.microsoft.com/fwlink/?LinkId=131685)|Este método libera el objeto SQLXML y los recursos que contiene.|  
|[InputStream getBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131754)|Devuelve un flujo de entrada para leer datos desde SQLXML.|  
|[Reader getCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131755)|Devuelve los datos **XML** como un objeto java.io.Reader o como un flujo de caracteres.|  
|[T extends Source T getSource(Class\<T> sourceClass)](https://go.microsoft.com/fwlink/?LinkId=131756)|Devuelve un **origen** para leer el valor **XML** que este objeto **SQLXML** especifica.<br /><br /> **Nota:**  El método getSource es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource y java.io.InputStream.|  
|[String getString()](https://go.microsoft.com/fwlink/?LinkId=131757)|Devuelve una representación de cadena del valor **XML** designado por este objeto SQLXML.|  
|[OutputStream setBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131758)|Recupera un flujo que se puede usar para escribir el valor **XML** que representa este objeto SQLXML.|  
|[Writer setCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131759)|Devuelve un flujo que se va a usar para escribir el valor **XML** que representa este objeto SQLXML.|  
|[T extends Result T setResult(Class\<T> resultClass)](https://go.microsoft.com/fwlink/?LinkId=131760)|Devuelve un **resultado** para establecer el valor **XML** que este objeto **SQLXML** especifica.<br /><br /> **Nota:** El método setResult es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult y java.io.OutputStream.|  
|[void setString(String value)](https://go.microsoft.com/fwlink/?LinkId=131762)|Establece el valor XML designado por este objeto SQLXML para la representación **String** especificada.|  
  
Las aplicaciones pueden leer y escribir valores XML en o desde un objeto SQLXML solamente una vez.  
  
Cuando se llama al método free(), un objeto SQLXML se vuelve no válido y no puede ser leído ni escrito. Si la aplicación intenta invocar a un método que no sea free() en ese objeto SQLXML, se genera una excepción.  
  
El objeto SQLXML no puede ser leído ni escrito cuando la aplicación llama a cualquiera de los siguientes métodos captador: getSource, getCharacterStream, getBinaryStream y getString.  
  
El objeto SQLXML no puede ser leído ni escrito cuando la aplicación llama a cualquiera de los siguientes métodos establecedor: setResult, setCharacterStream, setBinaryStream y setString.  
  
## <a name="see-also"></a>Consulte también  

[Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)  
