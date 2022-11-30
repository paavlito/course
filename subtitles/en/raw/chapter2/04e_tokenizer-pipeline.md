The tokenizer pipeline. In this video, we'll look at how a tokenizer converts raw text to numbers that a Transformer model can make sense of, like when we execute this code. Here is a quick overview of what happens inside the tokenizer object: first the text is split into tokens, which are words, parts of words, or punctuation symbols. Then the tokenizer adds potential special tokens and converts each token to their unique respective ID as defined by the tokenizer's vocabulary. As we'll see it doesn't actually happen in this order, but viewing it like this is better for understanding what happens. The first step is to split our input text into tokens with the tokenize method. To do this, the tokenizer may first perform some operations like lowercasing all words, then follow a set of rules to split the result in small chunks of text. Most of the Transformers models use a subword tokenization algorithm, which means that one given word can be split in several tokens, like tokenize here. Look at the "Tokenization algorithms" videos linked below for more information! The ## prefix we see in front of ize is the convention used by BERT to indicate this token is not the beginning of a word. Other tokenizers may use different conventions however: for instance ALBERT tokenizers will add a long underscore in front of all the tokens that had a space before them, which is a convention used by sentencepiece tokenizers. The second step of the tokenization pipeline is to map those tokens to their respective IDs as defined by the vocabulary of the tokenizer.  This is why we need to download a file when we instantiate a tokenizer with the from_pretrained method: we have to make sure we use the same mapping as when the model was pretrained. To do this, we use the convert_tokens_to_ids method. You may have noticed that we don't have the exact same result as in our first slide — or not, as this looks like a list of random numbers, in which case allow me to refresh your memory. We had a number at the beginning and at the end that are missing, those are the special tokens. The special tokens are added by the prepare_for_model method, which knows the indices of those tokens in the vocabulary and just adds the proper numbers. You can look at the special tokens (and more generally at how the tokenizer has changed your text) by using the decode method on the outputs of the tokenizer object. As for the prefix for beginning of words/part of words, those special tokens vary depending on which tokenizer you are using. The BERT tokenizer uses [CLS] and [SEP] but the roberta tokenizer uses html-like anchors <s> and </s>. Now that you know how the tokenizer works, you can forget all those intermediaries methods and only remember that you just have to call it on your input texts. The inputs don't contain the inputs IDs however, to learn what the attention mask is, check out the "Batch inputs together" video. To learn about token type IDs, look at the "Process pairs of sentences" video.