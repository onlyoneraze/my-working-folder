<!----- Conversion time: 1.019 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β17
* Wed Sep 18 2019 01:22:59 GMT-0700 (PDT)
* Source doc: https://docs.google.com/open?id=13Bwj-zrzPHWxDyeuZUzSwTNSqtZj9FI-spwD9tnhUTA
----->


## Простейшие TCP-клиент и эхо-сервер

### Цель работы

Познакомиться с приемами работы с сетевыми сокетами в языке программирования Python.

### Задания для выполнения

1. Создать простой TCP-сервер, который принимает от клиента строку (порциями по 1 КБ) и возвращает ее. (Эхо-сервер). ✓

![image](https://user-images.githubusercontent.com/70547060/138313612-3638fd10-454d-46ff-96b2-9aa3407f386f.png)

2. Сервер должен выводить в консоль служебные сообщения (с пояснениями) при наступлении любых событий: 
    1. Запуск сервера; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313202-97313732-d9ce-4e5b-8363-e71b3d9fa88c.png)
    
    2. Начало прослушивания порта; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313241-81ba89b2-4c85-44db-9534-09c9cf00af84.png)

    3. Подключение клиента; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313266-277d1309-4a6a-4634-988c-ce081532defe.png)
    
    4. Прием данных от клиента; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313334-9359880e-2beb-4452-bf7e-bb8060b7912f.png)
    
    5. Отправка данных клиенту; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313377-8e8ccee2-931b-434e-b4b3-08913d7b1bad.png)
    
    6. Отключение клиента; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313433-5985fa4b-1d14-4b2e-9873-15bd92688839.png)
    
    7. Остановка сервера. ✓

    ![image](https://user-images.githubusercontent.com/70547060/138313460-2242ccd7-057e-432e-8b94-29c897c0e144.png)

3. Напишите простой TCP-клиент, который устанавливает соединение с сервером, считывает строку со стандартного ввода и посылает его серверу. ✓

![image](https://user-images.githubusercontent.com/70547060/138313652-772df047-4061-4528-8422-b8d0120debad.png)

4. Клиент должен выводить в консоль служебные сообщения (с пояснениями) при наступлении любых событий: 
    1. Соединение с сервером; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313716-780350db-5548-4beb-8626-b11daf962cb4.png)
    
    2. Разрыв соединения с сервером; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313735-bb574967-2b31-42f1-9042-e1a1f19aa8b8.png)
    
    3. Отправка данных серверу; ✓
    
    ![image](https://user-images.githubusercontent.com/70547060/138313798-728bd3b8-812e-4b9e-98f7-5921ac256430.png)
    
    4. Прием данных от сервера. ✓

    ![image](https://user-images.githubusercontent.com/70547060/138313819-927b6878-c08c-49c4-a75a-7cd109ef8edc.png)

### Контрольные вопросы

1. Чем отличаются клиентские и серверные сокеты? 

   Клиентские сокеты грубо можно сравнить с конечными аппаратами телефонной сети, а серверные — с коммутаторами. Клиентское приложение (например, браузер) использует только клиентские сокеты, а серверное (например, веб-сервер, которому браузер посылает запросы) — как клиентские, так и серверные сокеты.

2. Как можно передавать через сокеты текстовую информацию? 

   Для того, чтобы мы могли общаться, нам необходимо знать адрес компьютера, на котором запущен процесс, и номер порта, по которому будет происходить обмен.

3. Какие операции с сокетами блокируют выполнение программы?

	```python
	conn, addr = sock.accept()
	data = conn.recv(1024)
	data = sock.recv(1024)
	```

4. Что такое неблокирующие сокеты? 

   Сокеты бывают блокирующие и неблокирующие. Суть в том, что в случае блокирующих сокетов при попытке прочитать (и записать) данные функция чтения будет ждать до тех пор, пока не прочитает хотя бы один байт или произойдет разрыв соединения или придет сигнал. В случае неблокирующих сокетов функция чтения проверяет, есть ли данные в буфере, и если есть - сразу возвращает, если нет, то она не ждет и также сразу возвращает, что прочитано 0 байт.

5. В чем преимущества и недостатки использования TCP по сравнению с UDP?

   Протокол TCP (Transmission Control Protocol) – это сетевой протокол, который «заточен» под соединение. Иными словами, прежде, чем начать обмен данными, данному протоколу требуется установить соединение между двумя хостами. Данный протокол имеет высокую надежность, поскольку позволяет не терять данные при передаче, запрашивает подтверждения о получении от принимающей стороны и в случае необходимости отправляет данные повторно. При этом отправляемые пакеты данных сохраняют порядок отправки, то есть можно сказать, что передача данных упорядочена. Минусом данного протокола является относительно низкая скорость передачи данных, за счет того что выполнение надежной и упорядоченной передачи занимает больше времени, чем в альтернативном протоколе UDP.

   Протокол UDP (User Datagram Protocol), в свою очередь, более прост. Для передачи данных ему не обязательно устанавливать соединение между отправителем и получателем. Информация передается без предварительной проверки готовности принимающей стороны. Это делает протокол менее надежным – при передаче некоторые фрагменты данных могут теряться. Кроме того, упорядоченность данных не соблюдается – возможен непоследовательный прием данных получателем. Зато скорость передачи данных по данному транспортному протоколу будет более высокой.

6. Какие системные вызовы, связанные с сокетами используются только на стороне сервера?

	```python
	sock.bind(('', port))
	sock.listen(0)
	conn, addr = sock.accept()
	data = conn.recv(1024)
	conn.send(data)
	conn.close()
	```

7. На каком уровне модели OSI работают сокеты? 

   На сеансовом (5) уровне. Хотя Идентификатор соединения (сокет) описывается на 4 уровне, нет чёткого указания, где именно он инициируется.

### Задания для самостоятельного выполнения

3. Модифицируйте код сервера таким образом, чтобы при разрыве соединения клиентом он продолжал слушать данный порт и, таким образом, был доступен для повторного подключения.

   ![image](https://user-images.githubusercontent.com/70547060/138322682-af685faa-febe-4790-961e-8b4c1ea8d36c.png)

4. Модифицируйте код клиента и сервера таким образом, чтобы номер порта и имя хоста (для клиента) они спрашивали у пользователя. Реализовать безопасный ввод данных и значения по умолчанию.

   ![image](https://user-images.githubusercontent.com/70547060/138323050-07e8d5dd-5611-441a-9645-a9e9b7be783a.png)

5. Модифицировать код сервера таким образом, чтобы все служебные сообщения выводились не в консоль, а в специальный лог-файл.

   Вот функция для записи в лог-файл:
   
   ```python
   def print_log(msg, clr = False):
	   func = {True: 'w', False: 'a'} # запись и дозапись соответственно
	   with open('logs.txt', func[clr], encoding='utf8') as f:
		   print(msg, file = f)
   ```

6. Модифицируйте код сервера таким образом, чтобы он автоматически изменял номер порта, если он уже занят. Сервер должен выводить в консоль номер порта, который он слушает.

   ```python
   port = 9090
   ready = False
   while not ready:
        try:
		    sock.bind(('', port))
		    ready = True
		    print(f'{port}')
	    except:
		    pport = port
		    port = random.randint(1000, 9999)
   ```

7. Реализовать сервер идентификации. Сервер должен принимать соединения от клиента и проверять, известен ли ему уже этот клиент (по IP-адресу). Если известен, то поприветствовать его по имени. Если неизвестен, то запросить у пользователя имя и записать его в файл. Файл хранить в произвольном формате.

	Чтение данных из файла
	```python
	userinfo = {}
		with open('clients.txt', 'r') as file:
			for line in file.readlines():
				userinfo = eval(line)
	```
	
	Запись данных в файл
	```python
	userinfo[addr[0]] = data.decode()
		with open('clients.txt', 'w') as file:
			print(userinfo, file = file)
	```

	![image](https://user-images.githubusercontent.com/70547060/138339524-0bf00039-7f93-47eb-93ba-9f38a0b65517.png)

	![image](https://user-images.githubusercontent.com/70547060/138339246-44f389c4-f520-4319-b844-2fa17315d5e7.png)

8. Реализовать сервер аутентификации. Похоже на предыдущее задание, но вместе с именем пользователя сервер отслеживает и проверяет пароли. Дополнительные баллы за безопасное хранение паролей. Дополнительные баллы за поддержание сессии на основе токена наподобие cookies

	Функция регистрации на сервере
	```python
	def s_register(conn, addr):
		try:
			conn.send(f'регистрация'.encode())
			data = conn.recv(1024)
			login = data.decode()
			data = conn.recv(1024)
			passw = data.decode()

			# хеширование
			salt = os.urandom(32)
			key = hashlib.pbkdf2_hmac(
				'sha256',
				passw.encode('utf-8'),
				salt,
				100000
			)

			userinfo[addr[0]] = [login, salt+key]
			conn.send('успешно'.encode())
			with open('clients.txt', 'w') as file:
				print(userinfo, file = file)
		except:
			conn.send('что-то пошло не так'.encode())
	```
	
	Функция авторизации на сервере
	```python
	def s_login(conn, addr):
		try:
			conn.send(f'логин'.encode())
			data = conn.recv(1024)
			login = data.decode()
			data = conn.recv(1024)
			passw = data.decode()

			# проверка пароля по ключу и хешу
			new_key = hashlib.pbkdf2_hmac(
				'sha256',
				passw.encode('utf-8'),
				userinfo[addr[0]][1][:32],
				100000
			)

			if new_key == userinfo[addr[0]][1][32:] and login == userinfo[addr[0]][0]:
				conn.send('успешно'.encode())
			else:
				conn.send('неправильные данные'.encode())
		except:
			conn.send('что-то пошло не так'.encode())
	```
	
	Функция регистрации на клиенте
	```python
	def c_register():
		print('Регистрация.')
		login = input('Введите логин: ')
		sock.send(login.encode())
		passw = input('Введите пароль: ')
		sock.send(passw.encode())
		data = sock.recv(1024)
		if 'успешно' in data.decode():
			print('Успешная регистрация!')
		else:
			print('Что-то пошло не так.')
	```
	
	Функция авторизации на клиенте
	```python
	def c_login():
		print('Авторизация.')
		login = input('Введите логин: ')
		sock.send(login.encode())
		passw = input('Введите пароль: ')
		sock.send(passw.encode())
		data = sock.recv(1024)
		if 'успешно' in data.decode():
			print('Успешная авторизация!')
		else:
			print('Неверные логин или пароль.')
	```
	
	Пример хранения пароля
	```python
	{'192.168.1.2': ['zxc', b'\xfejn\x00V\xa2D\x9d\x86\xc0\xe8\xc5\xa4=K\x14\xa9\xa8\xb0\xabi\x9a=\x0b\x02\xcck\xe0\xd9l/l\x10\xec\x178G4h@/W\xfc@\xad\xcc(\xfc\xc0\xcb@\xb1\xbdN\xd9d\xa7\x89\xdfKq\xae\x7f5']}
	```
	
	![image](https://user-images.githubusercontent.com/70547060/138340061-5d2cc2e0-d907-43ab-9ad6-10e6c6972ab2.png)

	![image](https://user-images.githubusercontent.com/70547060/138340123-d498099b-a185-45ca-bad5-05c798810aee.png)

	![image](https://user-images.githubusercontent.com/70547060/138340169-438004b7-367a-4545-a485-5aed157a132d.png)

9. Напишите вспомогательные функции, которые реализуют отправку и принятие текстовых сообщений в сокет. Функция отправки должна дополнять сообщение заголовком фиксированной длины, в котором содержится информация о длине сообщения. Функция принятия должна читать сообщение с учетом заголовка. В дополнении реализуйте преобразование строки в байтовый массив и обратно в этих же функциях. Дополнително оценивается, если эти функции будут реализованы как унаследованное расширение класса socket библиотеки socket.

	Вспомогательные функции сервера:
	```python
	def s_send(sock, data, service_data=''):
		data = bytearray(f'{len(data)}$@$~{data}{service_data}'.encode())
		sock.send(data)

	def s_recv(sock):
		data = sock.recv(1024).decode()
		indx = data.find('$@$~')
		atkn = re.search('\$token=(.{32,32})\$', data)
		if atkn:
			data = data[:atkn.start()]
			atkn = atkn[1]
		else:
			atkn = ''
		print('Recieved message length - {}'.format(data[:indx]))
		return data[indx+4:], atkn
	
	socket.socket.s_send = s_send
	socket.socket.s_recv = s_recv
	```
	
	Вспомогательные функции клиента:
	```python
	def s_send(sock, data, token = ''):
		data = bytearray(f'{len(data)}$@$~{data}$token={token}$'.encode())
		sock.send(data)

	def s_recv(sock):
		data = sock.recv(1024).decode()
		indx = data.find('$@$~')
		pswd = data.rfind('$$$~')
		answ = data.rfind('@$$~')
		atkn = re.search('\$token=(.{32,32})\$', data)

		print('Recieved message length - {}'.format(data[:indx]))

		if pswd>-1:
			return data[indx+4:pswd], 1

		elif answ>-1:
			return data[indx+4:answ], 2

		elif atkn:
			indx2 = atkn.start()

			return (data[indx+4:indx2], atkn[1]), 3
		else:
			return data[indx+4:], 0
	
	socket.socket.s_send = s_send
    socket.socket.s_recv = s_recv
	```
	
	Функции сделаны унаследованным расширением класса socket библиотеки socket. Также присутствует преобразование строки в байтовый формат и наоборот. И, конечно же, длина сообщения.
	
	![image](https://user-images.githubusercontent.com/70547060/138348368-0286d806-9629-4bc8-83f4-cce0721869d0.png)
	
10. Дополните код клиента и сервера таким образом, чтобы они могли посылать друг другу множественные сообщения один в ответ на другое.

	![image](https://user-images.githubusercontent.com/70547060/138348438-f196ef5b-164b-4f8e-b85f-f66e57a9f6ba.png)


#### Дополнительные задания 3 - 6 реализованы в папке "Модифицированная версия эхо сервера". 

#### Дополнительное задание 7 реализовано в папке "Сервер идентификации". 

#### Дополнительное задание 8 реализовано в папке "Сервер аутентификации".

#### Дополнительные задания 9 - 10 реализованы в папке "Мини-чат со вспомогательными функциями".

<!-- Docs to Markdown version 1.0β17 -->
