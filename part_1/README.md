# README

## Để bắt đầu
Di chuyển vào thư mục chứa file README.md này

```bash
docker-compose up
```

## Tạo quyền và gán quyền cho user trong MySQL

```
GRANT ALL PRIVILEGES ON sakila.*  TO 'hdfs_part_1'@'%';
CREATE DATABASE sakila
```

## Lệnh để tải và import dữ liệu mẫu vào MySQL

```bash
curl -Lo ./sakila-db.zip http://downloads.mysql.com/docs/sakila-db.zip
unzip ./sakila-db.zip
cat sakila-db/sakila-schema.sql | docker exec -i mysql_hdfs_part_1 mysql -u hdfs_part_1 --password=hdfs_part_1 sakila
cat sakila-db/sakila-data.sql | docker exec -i mysql_hdfs_part_1 mysql -u hdfs_part_1 --password=hdfs_part_1 sakila

rm -rf unzip sakila-db

# Kiểm tra dữ liệu
docker exec -i mysql_hdfs_part_1 mysql -u hdfs_part_1 --password=hdfs_part_1 -e "select film_id, title from sakila.film limit 1"

```
