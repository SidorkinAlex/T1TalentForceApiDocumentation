# Кандидаты

Используется стандартное [API Suite CRM](https://docs.suitecrm.com/developer/api/developer-setup-guide/)
1.  [Получение оффера кандидата (.bin)](#get_binary_offer)

<a name="get_binary_offer"></a>
## Получение оффера кандидата (.bin)

Предварительно необходимо [зарегистрировать](https://talentforce.ru/) приложение.

Добавить в запрос полученный при авторизации access_token

* **Запрос**

Необходимо отправить GET-запрос на:

`{{talentforce.url}}Api/V8/binary_offer/vacancyId/candidateId`

где 

 vacancyId - ID вакансии, по которой сформирован оффер
 candidateId - ID кандидата

Пример: {{talentforce.url}}/Api/V8/binary_offer/62ff37e3-cc68-eee2-7209-5fcf1019eba4/2c97ac19-7d66-6ea4-af07-61b9c62d320d


* **Пример ответа**

Статус 200

```text
%PDF-1.4
%����
3 0 obj
<</Type /Page
/Parent 1 0 R
/MediaBox [0 0 595.280 841.890]
/TrimBox [0.000 0.000 595.280 841.890]
/Resources 2 0 R
/Group << /Type /Group /S /Transparency /CS /DeviceRGB >> 
/Contents 4 0 R>>
endobj
4 0 obj
<</Filter /FlateDecode /Length 1135>>
stream
x��W[OG��}�[�V}h�*UJ�2�egw�`�q�$���H}h�A�Z�#R�~�93cX�Kid�egv���w.3�R���TJ�/����\�RZ<��k�4�m%svC���4���������dLǗ�k�<Ӎ���U�j�1�@�s��>��]MZ��Gi�秝(c�������K<�����7���';�z]:i�Ǔ"cXz�R�*���+���OP����^�.�PV=�ONa>H�kU�J5ttB�\�#�-�.~;��:��Ztv:�Hy���F:�*���4�����*�K+��[I�{�XmMb�ng��x��=G����!��D�@��s��]�+1���H��Ťݡ&�d�Z,"��d������
�S�Z?EMJBWJWڄ^'$z����ۓc��!�4)i�E_o�V�d�|�Z|[��D�+<��R�C�_Ī(���X�����;��#i�*�[|_�*t1�zWl`��Pª)<�no�I�0��0���n�/6�M���>�s�X�F3,i�r���LVе	m{�x��,HpX�ό]l�k��6`kV
���y��x�Cm��Y�k�m3����h%V�ae�
```
