## **Code Peer Review Templete**
------------------
- 코더 : 박재영
- 리뷰어 : 김설아

## **PRT(PeerReviewTemplate)**  
------------------  
- [x] **1. 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?**
- [x] **2. 주석을 보고 작성자의 코드가 이해되었나요?**  
  
```python
print(maxlen)       # 문장 최대 길이 : 75, 99% 커버 
print(vocab_size)    # 단어집 사이즈  : 10000개 테스트 
print(word_vector_dim) # 차원 :16
```

```python
lstm_model.add(tf.keras.layers.LSTM(64))                        # 8 - 과적합 현상 발생 -> 16 -> 64 로 조정
```  
  
변수에 대한 설명, 설정값 선정 이유 등을 자세하게 설명해주셨습니다.


- [x] **3. 코드가 에러를 유발할 가능성이 있나요?**
  
```python
list_len = []
for l_list in [X_train,X_test]:
    list_len += get_list_length(l_list)

```
리스트를 for문 밖에 선언하여 중첩되는 오류가 발생할 수 있는 상황을 만들지 않았습니다.  


- [x] **4. 코드 작성자가 코드를 제대로 이해하고 작성했나요?**  
  
```python
early_stop = EarlyStopping(monitor='accuracy', mode='min', verbose=1, patience=4)    # 10-> 5-> 4 로 조정

dcnn_model.compile(optimizer='adam',
              loss='binary_crossentropy',
              metrics=['accuracy'])
              
epochs=50  

history = dcnn_model.fit(partial_x_train,
                    partial_y_train,
                    epochs=epochs,
                    batch_size=512,
                    validation_data=(x_val, y_val),
                    verbose=1,
                    callbacks=[early_stop])
```
과적합이 일어나기 쉬운 모델의 특성을 이해하고 파라미터를 조정하셨습니다.

- [x] **5. 코드가 간결한가요?**  
  
```python
model_dic = {'lstm_model':lstm_model,'dcnn_model':dcnn_model,'gmp_model':gmp_model}
model_list = list(model_dic.values())
model_name_list = list(model_dic.keys())
history_list = [lstm_history_dict,dcnn_history_dict ,gmp_history_dict]
```
딕셔너리 구조를 활용하여 리스트 생성을 정리하셨습니다.


## **참고링크**  
------------------  
- Facebook AI Research(FAIR) lab 에서 만든 단어 임베딩 및 텍스트 분류 학습을 위한 fastText를 사용하셨습니다.
https://en.wikipedia.org/wiki/FastText
    
