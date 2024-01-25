import streamlit as st
import pandas as pd
from wordcloud import WordCloud
import matplotlib.pyplot as plt
from collections import Counter
import io

# Streamlit 애플리케이션 시작
st.title('워드 클라우드 및 단어 빈도 분석')

# 파일 업로드
uploaded_file = st.file_uploader("CSV 파일 업로드", type="csv")
if uploaded_file is not None:
    # 파일 읽기
    data = pd.read_csv(uploaded_file)
    # 데이터 컬럼 선택
    column_name = st.selectbox('텍스트가 포함된 컬럼을 선택하세요', data.columns)
    text_data = data[column_name].dropna().values

    # 데이터 보기 옵션
    if st.checkbox('데이터 보기'):
        st.write(data)

    # 불용어 설정
    exclude_words = set(['부산대', '부산', '서면', '해운대', '해운대맛집', '서면맛집', '맛집', '점', '추천', '맛있는'])

    # 워드클라우드 생성 함수
    def create_wordcloud(text_data):
        text = ' '.join(text_data)
        wordcloud = WordCloud(width = 800, height = 800, background_color ='white', stopwords = exclude_words, min_font_size = 10).generate(text)
        
        # 워드클라우드 표시
        plt.figure(figsize=(8, 8), facecolor=None)
        plt.imshow(wordcloud, interpolation='bilinear')
        plt.axis("off")
        st.set_option('deprecation.showPyplotGlobalUse', False)
        st.pyplot()

    # 워드클라우드 생성 버튼
    if st.button('워드클라우드 생성'):
        create_wordcloud(text_data)

    # 단어 빈도 히스토그램 생성 함수
    def plot_histogram(text_data):
        word_count = Counter(" ".join(text_data).split()).most_common()
        words = [word[0] for word in word_count if word[0] not in exclude_words][:10]
        counts = [word[1] for word in word_count if word[0] not in exclude_words][:10]

        plt.figure(figsize=(10,5))
        plt.bar(words, counts)
        plt.xlabel('Words')
        plt.ylabel('Frequency')
        plt.xticks(rotation=45)
        plt.title('Word Frequency Histogram')
        st.pyplot()

    # 단어 빈도 히스토그램 생성 버튼
    if st.button('히스토그램 그리기'):
        plot_histogram(text_data)

