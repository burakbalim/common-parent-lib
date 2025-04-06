# Common Parent Library (BOM)

Bu proje, mikroservis mimarisinde kullanılmak üzere bir Bill of Materials (BOM) sağlar. BOM, bağımlılık versiyonlarını merkezi bir şekilde yönetmek için kullanılır.

## BOM Avantajları

- **Merkezi Sürüm Yönetimi**: Tüm mikroservislerde aynı bağımlılık sürümlerini kullanmayı sağlar
- **Tutarlılık**: Projenizin tüm modüllerinde tutarlı yapılandırma sunar
- **Kolay Güncelleme**: Bağımlılık sürümlerini tek bir yerde güncelleyerek tüm projeyi etkileyebilirsiniz

## Kullanım

Bu BOM'u kullanmak için, Maven projenizin `pom.xml` dosyasındaki `dependencyManagement` bölümüne aşağıdaki gibi ekleyin:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.thales</groupId>
            <artifactId>common-parent-lib</artifactId>
            <version>0.0.1-SNAPSHOT</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Daha sonra, BOM'da tanımlanan bağımlılıkları sürüm belirtmeden kullanabilirsiniz:

```xml
<dependencies>
    <!-- Common Library -->
    <dependency>
        <groupId>com.thales</groupId>
        <artifactId>common-lib</artifactId>
        <!-- Sürüm gerekli değil, BOM'dan geliyor -->
    </dependency>
    
    <!-- Auth Security Library -->
    <dependency>
        <groupId>com.thales</groupId>
        <artifactId>auth</artifactId>
        <!-- Sürüm gerekli değil, BOM'dan geliyor -->
    </dependency>
    
    <!-- MapStruct -->
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
        <!-- Sürüm gerekli değil, BOM'dan geliyor -->
    </dependency>
</dependencies>
```

## Parent Olarak Kullanım

BOM'u diğer projelerin parent'ı olarak da kullanabilirsiniz:

```xml
<parent>
    <groupId>com.thales</groupId>
    <artifactId>common-parent-lib</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</parent>
```

Bu şekilde, BOM'da tanımlanan tüm yapılandırma ve plugin ayarlarını da miras alırsınız.

## Derleme

BOM'u derlemek için:

```bash
cd common-parent-lib
mvn clean install
```

## BOM'da Tanımlanan Önemli Sürümler

- Java: 21
- Spring Boot: 3.2.5
- Spring Cloud: 2023.0.5
- MapStruct: 1.5.5.Final
- TestContainers: 1.19.3
- Auth Security Library: 1.0.1
- Hibernate Types (JSONB): 2.21.1
- SpringDoc OpenAPI: 2.6.0

## Plugin Yönetimi

BOM'da tanımlanan önemli plugin yapılandırmaları:

1. **Maven Compiler Plugin**: Java 21, Lombok ve MapStruct için annotation işlemcileri
2. **JaCoCo Plugin**: Test kapsamı raporları için
3. **Maven Surefire Plugin**: Test çalıştırma yapılandırması

## GitHub Packages'a Yayınlama

Bu BOM'u GitHub Packages'a yayınlamak için:

```bash
mvn deploy -DskipTests
```

**Not**: GitHub Packages'a yayınlama için gerekli yapılandırmaları `settings.xml` dosyanıza eklemelisiniz. 