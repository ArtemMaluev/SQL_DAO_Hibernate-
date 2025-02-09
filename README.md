# ������ ��� ������� � Hibernate

## ��������
��������� ���������� �� [DAO ����](../../jdbc/task1/README.md) �� Hibernate.

1. ��� ���������� ����� �������� ��� `Entity`, ��������������� ���� �������� �� �������. ������, ��� ��� ���� ����� ����� ������� ������ ��������� ���� Entity: `OneToOne`, `OneToMany`, `ManyToOne`, `ManyToMany`

2. ���������� �����������, ����� �� ������ ������� � `EntityManager`, � �� ����� `NamedParameterJdbcTemplate`.

# ������ DAO ����

## ��������
�������������� � ������ � Spring JDBC, ������� ��������� ��� ���������� ����. ��� ���� �������� ���������� ��� ������ � ��, ��������� �������, ������� �� �������� �� [������ �������](../../sql-agg/task/README.md)

1. �������� spring boot ����������, � ������������� �� ��� starter'� - `spring-boot-starter-jdbc` � `spring-boot-starter-web`

2. ���������� ������ �������� ������� � ���� `schema.sql`, ����� spring boot ������������� �������� �������.

2. ���������� ������ ������� �� ������� ������� � ����� `resources`. ���������� ������ ���, ����� ��� ��������� `product_name` ��� ������������ ��������� `name`(� �� ������ ��� `alexey`), ������� �� ������ ���������� � ������ ���������� ������� `NamedParameterJdbcTemplate` ������ �� �������� �������.

3. �������� ����������� ��� ������ � ��. ��� �����:
 - �������� ����� � �������� ��� ���������� Repository, ���� �������� ��� ����������� � Java config ������
 - �������� � ���� ������ String, ������� �������� ���� ���������� ������ �������. ���� ���������� �� ������ ������� � ������� ���� ����. ��� ���� ����� �������� � ����� `read` �������� ������ �������, ������� ����� � ����� `resources`. �������� ���: `read(myScript.sql)`.
 - �������� ����� `getProductName(String name)`, ������� ����� ��������� ��� � ���������� �������� �������� �� ���� ������.
```java
private static String read(String scriptFileName) {
        try (InputStream is = new ClassPathResource(scriptFileName).getInputStream();
             BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(is))) {
            return bufferedReader.lines().collect(Collectors.joining("\n"));
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
``` 

4. �������� ����������, � �������-������������ GET-������ ������� � ��������� �� endpoint `/products/fetch-product`. � query params ������� ����� ��������� ��������� �������� `name`, ������� ��� ���� ����� ���������� ������ � �����������. �� ����, ��� ����� ������ ����� ������������ ������ ���� `localhost:8080/products/fetch-product?name=Ivan`.
���������� ������ ����� ���������� �������� ��������, ������� �� ������� �� �����������.
