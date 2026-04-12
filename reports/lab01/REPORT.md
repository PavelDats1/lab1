# Laboratory Work 01

## Student Info
- **Name:** Павел Дацковских
- **GitHub:** PavelDats1
- **Group:** ИУ8-21

## Tutorial (выполненные команды)

### 1. Настройка окружения
```bash
export GITHUB_USERNAME="PavelDats1"
export GIST_TOKEN="[токен]"
alias edit=nano

mkdir -p ~/${GITHUB_USERNAME}/workspace
cd ~/${GITHUB_USERNAME}/workspace
pwd
# Output: /home/pavel/PavelDats1/workspace

mkdir -p workspace/tasks/
mkdir -p workspace/projects/
mkdir -p workspace/reports/
cd workspace
pwd
# Output: /home/pavel/PavelDats1/workspace/workspace
```
### 2. Установка Node.js
```bash
wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
tar -xf node-v6.11.5-linux-x64.tar.xz
rm -rf node-v6.11.5-linux-x64.tar.xz
mv node-v6.11.5-linux-x64 node

ls node/bin
# Output: node  npm  npx

export PATH=${PATH}:`pwd`/node/bin
echo ${PATH}
# Output: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/pavel/PavelDats1/workspace/workspace/node/bin
```
### 3. Установка gist
```bash
mkdir scripts
cat > scripts/activate <<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
source scripts/activate

sudo gem install gist
(umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```
### 4. Клонирование лабораторной работы
```bash
export LAB_NUMBER=01
git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
# Репозиторий склонирован в ~/PavelDats1/workspace/tasks/lab01
```
### 5. Подготовка отчета
```bash
mkdir -p reports/lab${LAB_NUMBER}
cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
cd reports/lab${LAB_NUMBER}
pwd
# Output: /home/pavel/PavelDats1/workspace/reports/lab01
```
## Homework

### 1. Скачивание и распаковка Boost
```bash
cd ~
wget -O boost_1_69_0.tar.gz https://archives.boost.io/release/1.69.0/source/boost_1_69_0.tar.gz
tar -xzf boost_1_69_0.tar.gz
mv boost_1_69_0 ~/PavelDats1/workspace/
```
### 2. Подсчет файлов в корневой директории
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -maxdepth 1 -type f | wc -l
#Output: 12
```
### 3. Подсчет всех файлов
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -type f | wc -l
#Output: 61191
>**Полный список всех файлов:** [`file_lists/all_files.txt`](https://github.com/PavelDats1/lab1/blob/main/file_lists/all_files.txt)
```
### 4. Подсчет заголовочных файлов
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -type f \( -name "*.h" -o -name "*.hpp" -o -name "*.hh" \) | wc -l
###Output: 15208
>**Список заголовочных файлов:** [`file_lists/header_files.txt`](https://github.com/PavelDats1/lab1/blob/main/file_lists/header_files.txt)
```
### 5. Подсчет файлов .cpp
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -type f -name "*.cpp" | wc -l
#Output: 13774
```
### 6. Подсчет остальных файлов
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -type f -not \( -name "*.h" -o -name "*.hpp" -o -name "*.hh" -o -name "*.cpp" \) | wc -l
#Output: 32209
>**Список .cpp файлов:** [`file_lists/cpp_files.txt`](https://github.com/PavelDats1/lab1/blob/main/file_lists/cpp_files.txt)
```
### 7. Поиск файла any.hpp
```bash
find ~/PavelDats1/workspace/boost_1_69_0 -name "any.hpp" -type f
#Output: /home/pavel/PavelDats1/workspace/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/proto/detail/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/fusion/include/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/type_erasure/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/hana/fwd/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/hana/any.hpp
#/home/pavel/PavelDats1/workspace/boost_1_69_0/boost/any.hpp
>**Путь сохранен в:** [`search_results/any_path.txt`](https://github.com/PavelDats1/lab1/blob/main/search_results/any_path.txt)
 ```
### 8. Поиск упоминаний boost::asio
```bash
grep -r "boost::asio" ~/PavelDats1/workspace/boost_1_69_0 > ~/PavelDats1/workspace/search_results/boost_asio_full.txt
#Output: Всего строк: 4152
>**Полный результат поиска:** [`search_results/boost_asio_full.txt`](https://github.com/PavelDats1/lab1/blob/main/search_results/boost_asio_full.txt)
```
### 9. Компиляция Boost
```bash
cd ~/PavelDats1/workspace/boost_1_69_0
./bootstrap.sh --prefix=~/PavelDats1/workspace/boost_1_69_0/build
./b2 install
```
### 10. Перенос библиотек в директорию
```bash
mkdir -p ~/boost-libs
find ~/PavelDats1/workspace/boost_1_69_0 -name "*.a" -type f -exec cp {} ~/boost-libs/ \;
#Output: Все библиотеки успешно скопированы
```
### 11. Размер каждого файла 
```bash
cd ~/boost-libs
du -h *
#Output:
#4.0K	libboost_atomic.a
#236K	libboost_chrono.a
#148K	libboost_container.a
#24K	libboost_context.a
#332K	libboost_contract.a
#152K	libboost_date_time.a
#4.0K	libboost_exception.a
#232K	libboost_fiber.a
#416K	libboost_filesystem.a
#848K	libboost_graph.a
#172K	libboost_iostreams.a
#2.0M	libboost_locale.a
#544K	libboost_math_c99.a
#448K	libboost_math_c99f.a
#464K	libboost_math_c99l.a
#2.7M	libboost_math_tr1.a
#2.6M	libboost_math_tr1f.a
#2.7M	libboost_math_tr1l.a
#212K	libboost_prg_exec_monitor.a
#1.6M	libboost_program_options.a
#80K	libboost_random.a
#2.7M	libboost_regex.a
#1.2M	libboost_serialization.a
#24K	libboost_stacktrace_addr2line.a
#20K	libboost_stacktrace_backtrace.a
#16K	libboost_stacktrace_basic.a
#4.0K	libboost_stacktrace_noop.a
#4.0K	libboost_system.a
#2.3M	libboost_test_exec_monitor.a
#56K	libboost_timer.a
#2.3M	libboost_unit_test_framework.a
#4.5M	libboost_wave.a
#796K	libboost_wserialization.a
```
### 11. Топ 10 самых тяжелых файлов
```bash
cd ~/boost-libs
du -h * | sort -hr | head -10
###Output:
#4.5M	libboost_wave.a
#2.7M	libboost_regex.a
#2.7M	libboost_math_tr1l.a
#2.7M	libboost_math_tr1.a
#2.6M	libboost_math_tr1f.a
#2.3M	libboost_unit_test_framework.a
#2.3M	libboost_test_exec_monitor.a
#2.0M	libboost_locale.a
#1.6M	libboost_program_options.a
#1.2M	libboost_serialization.a
>**Результат сохранен в:** [`file_lists/top10_libs.txt`](https://github.com/PavelDats1/lab1/blob/main/file_lists/top10_libs.txt)
```

