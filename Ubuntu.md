## Launch 2 VM machines (Namely- Monitoring Tool, Website)

## Machine -1 (Monitoring Tool)
## Step 1: Install wget and tar Packages
```xml
sudo apt update -y
sudo apt install wget tar
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz
```

## Step  : 
```xml
tar xvfz node_exporter-1.8.1.linux-amd64.tar.gz
```

## Step  : 
```xml
mv node_exporter-1.8.1.linux-amd64/ node_exporter
```

## Step  : 
```xml
rm -rf node_exporter-1.8.1.linux-amd64.tar.gz
```

## Step  : 
```xml
cd node_exporter
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
sudo apt install openjdk-17-jre-headless -y
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
sudo apt install maven -y
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
sudo apt install git -y
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
git clone https://github.com/jaiswaladi246/Boardgame.git
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
cd Boardgame/
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
mvn package
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
cd target/
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
java -jar database_service_project-0.0.2.jar
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
cd ..
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
cd node_exporter/
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
ls
```

## Step  : Installing Node Exporter (1.8.1) in Machine-1
```xml
./node_exporter &
```

## Machine -2 (Website)

## Step 1 : Visit Prometheus Downloads Page
```xml
https://prometheus.io/download/
```

## Step 2 : Installing Prometheus (2.52.0V)
```xml
wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
```

## Step 3 : Installing Alert Manager (0.27.0V)
```xml
wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz
```

## Step 4 : Black Box Exporter (0.25.0)
```xml
wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.25.0/blackbox_exporter-0.25.0.linux-amd64.tar.gz
```



## Step 6 :
```xml

```

## Step 7 :
```xml

```

## Step 8 :
```xml

```

## Step 9 :
```xml

```

## Step 10 :
```xml

```

## Step 11 :
```xml

```

## Step 12 :
```xml

```

## Step 13 :
```xml




sudo apt update -y
    6  wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
    7  ls
    8  clear
    9  tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
   10  ls
   11  rm -rf prometheus-2.52.0.linux-amd64.tar.gz
   12  ls
   13  clear
   14  cd prometheus-2.52.0.linux-amd64/
   15  ls
   16  cd ..
   17  ls
   18  mv prometheus-2.52.0.linux-amd64/ prometheus
   19  ls
   20  wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.25.0/blackbox_exporter-0.25.0.linux-amd64.tar.gz
   21  ls
   22  tar xvfz blackbox_exporter-0.25.0.linux-amd64.tar.gz
   23  ls
   24  rm -rf blackbox_exporter-0.25.0.linux-amd64.tar.gz
   25  ls
   26  mv blackbox_exporter-0.25.0.linux-amd64/ blackbox_exporter
   27  ls
   28  clear
   29  wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz
   30  ls
   31  tar xvfz alertmanager-0.27.0.linux-amd64.tar.gz
   32  ls
   33  rm -rf alertmanager-0.27.0.linux-amd64.tar.gz
   34  mv alertmanager-0.27.0.linux-amd64/ alertmanager
   35  ls
   36  clear
   37  ls
   38  cd prometheus/
   39  ls
   40  ./prometheus &
   41  netstat -nltp
   42  sudo apt install net-tools
   43  netstat -nltp
   44  cd ..
   45  ls
   46  cd alertmanager/
   47  ls
   48  cd ..
   49  ls
   50  cd prometheus/
   51  ls
   52  clear
   53  ls
   54  vi alert_rules.yml
   55  ls
   56  clear
   57  ls
   58  vi prometheus.yml
   59  clear
   60  ls
   61  cat prometheus.yml
   62  cd ../alertmanager/
   63  ls
   64  ./alertmanager &
   65  cd ../prometheus/
   66  ls
   67  netstat -nltp
   68  pgrep prometheus
   69  kill 5391
   70  ./prometheus &
   71  vi prometheus.yml
   72  pgrep prometheus
   73  kill 16136
   74  ./prometheus &
   75  ls
   76  nano prometheus.yml
   77  vi prometheus.yml
   78  rm -rf prometheus.yml
   79  nano prometheus.yml
   80  cat prometheus.yml
   81  pgrep prometheus
   82  kill 24086
   83  ./prometheus &
   84  cd ..
   85  ls
   86  cd blackbox_exporter/
   87  ls
   88  ./blackbox_exporter &
   89  cd ..
   90  ls
   91  cd alertmanager/
   92  ls
   93  nano alertmanager.yml
   94  rm -rf alertmanager.yml
   95  ls
   96  clear
   97  nano alertmanager.yml
   98  vi alertmanager.yml
   99  pgrep prometheus
  100  pgrep alertmanager
  101  kill 14363
  102  ./alertmanager &
  103  cd ..
  104  ls
  105  cd prometheus/
  106  ls
  107  pgrep prometheus
  108  kill 29075
  109  ./prometheus &
  110  cd ..
  111  cd alertmanager/
  112  ls
  113  vi alertmanager
  114  vi alertmanager.yml
  115  pgrep alertmanager
  116  kill 44554
  117  ./alertmanager &
  118  cd ../prometheus/
  119  ls
  120  pgrep prometheus
  121  kill 44946
  122  ./prometheus &
  123  vi prometheus.yml
  124  nano prometheus.yml
  125  pgrep prometheus
  126  kill 54584
  127  ./prometheus &
  128  nano prometheus.yml
  129  pgrep prometheus
  130  ./prometheus &
  131  vi prometheus.yml
  132  nano prometheus.yml
  133  clear
  134  cat prometheus.yml
  135  celar
  136  clear
  137  mv prometheus.yml prometheus1.yml
  138  nano prometheus.yml
  139  cat prometheus.yml
  140  clear
  141  ls
  142  pgrep prometheus
  143  kill 62068
  144  ./prometheus &
  145  clear
  146  ls
  147  cd ..
  148  ls
  149  cd alertmanager/
  150  ls
  151  cat alertmanager.yml
  152  pgrep alertmanager
  153  kill 53922
  154  ./alertmanager &
  155  pgrep alertmanager
  156  cd ..
  157  clear
  158  ls
  159  cd blackbox_exporter/l
  160  cd blackbox_exporter/
  161  ls
  162  cat blackbox.yml
  163  cd ..
  164  ;s
  165  ls
  166  cd prometheus/
  167  ls
  168  cat prometheus.yml
  169  cd ..
  170  ls
  171  cd alertmanager/
  172  clear
  173  ls
  174  clear
  175  cat alertmanager.yml
  176  sudo apt install tar
  177  history

```

## Step 14 :
