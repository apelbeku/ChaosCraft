# Use the official PHP image with Apache
FROM php:8.1-fpm

# Install any necessary PHP extensions
RUN docker-php-ext-install pdo pdo_mysql

# Set the working directory
WORKDIR /var/www/html

# Copy the application source code
COPY ../src /var/www/html

# Expose port 9000
EXPOSE 9000