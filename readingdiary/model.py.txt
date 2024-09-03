from datetime import datetime


class Note:
    def __init__(self, text: str, page: int, date: datetime):
        self.text: str = text
        self.page: int = page
        self.date: datetime = date

    def __str__(self) -> str:
        return f"{self.date} - page {self.page}: {self.text}"


class Book:
    EXCELLENT: int = 3
    GOOD: int = 2
    BAD: int = 1
    UNRATED: int = -1

    def __init__(self, isbn: str, title: str, author: str, pages: int):
        self.isbn: str = isbn
        self.title: str = title
        self.author: str = author
        self.pages: int = pages
        self.rating: int = Book.UNRATED
        self.notes: list[Note] = []

    def add_note(self, text: str, page: int, date: datetime) -> bool:
        if page > self.pages:
            return False
        else:
            Note = [text, page, date]
            self.notes.append(Note)
            return True

    def set_rating(self, rating: int) -> bool:
        if not rating == Book.EXCELLENT or Book.GOOD or Book.BAD:
            self.rating = rating
            return True
        else:
            return False

    def get_notes_of_page(self, page: int) -> list[Note]:
        return Note[self.notes]

    def page_with_most_notes(self) -> int:
        pass

    def __str__(self) -> str:
        return f"ISBN: {self.isbn}\
                Title: {self.title}\
                Author: {self.author}\
                Pages: {self.pages}\
                Rating: {self.rating}"


class ReadingDiary:
    def __init__(self):
        self.books: dict[str, Book] = {}

    def add_book(self, isbn: str, title: str, author: str, pages: int) -> bool:
        if isbn not in self.books:
            Book = [isbn, title, author, pages]
            self.books.append(Book)
        else:
            return False

    def search_by_isbn(self, isbn: str) -> Book | None:
        pass

    def add_note_to_book(self, isbn: str, text: str, page: int, date: datetime) -> bool:
        pass

    def rate_book(self, isbn: str, rating: int) -> bool:
        book = self.search_by_isbn(isbn)
        if book is None:
            return False
        return book.set_rating(rating)

    def book_with_most_notes(self) -> Book | None:
        pass
